# Jora: Kafka and Redis plan

Oct 11, 2026 · @Hoang

## The one rule

Use Kafka when something happened and other parts must react to it later, without losing it. Use Redis when many app instances need a fast, short-lived shared memory. If a user is waiting for a quick database answer, use neither.

- **Kafka** is a durable log of events. Producers write facts like "job discovered". Consumers read them at their own speed, retry on failure, and can replay old events. It is the right tool for slow, failure-prone or fan-out work: crawling, LLM calls, emails.
- **Redis** is an in-memory store with expiry (TTL). Use it for caches, locks, rate limits, counters and "already done" markers. It is never the only copy of important data.
- **Neither** fits login, CRUD on search profiles, and paging through recommendations. Postgres already answers these in milliseconds.

AWS comes last. It hosts the same pieces as managed services: MSK for Kafka, ElastiCache for Redis, RDS for Postgres and S3 for resume files.

All of this applies to the code on main as of 767174a.

## Where each tool fits in Jora

Crawling, recommendations, email and resume tailoring belong on Kafka. Redis protects the crawler, the LLM budget and later the hot read paths.

| Work | How it runs today | Kafka | Redis | Why |
| --- | --- | --- | --- | --- |
| Crawl a job board | Admin POST, runs inside the request, `block()` per call | Yes: `crawl.requested`, keyed by board | Lock per board, rate limit per platform | External APIs are slow and fail. Two instances must not crawl the same board at once. |
| Fetch and save each posting | Loop inside `JobIngestionService` | Yes: `job.discovered`, one message per posting | No | One bad posting no longer kills the whole board. |
| Dedupe into canonical jobs | `JobPostingPersistenceService` | Yes: consumer emits `job.created` or `job.updated` | No | The Postgres unique key already makes it safe to run twice. |
| Generate recommendations | `POST /generate`, scores every job while the user waits | Yes: react to `job.created` and `searchprofile.updated`, emit `job.matched` | No | Cost grows with jobs × users. Do it in the background so reads stay fast. |
| Email new matches | Not built | Yes: consumer of `job.matched` | "Already emailed" marker, digest buffer | It must never send twice, and the mail server can be down. |
| Extract resume text (M6) | Being designed | Not yet | No | Small PDFs are fast enough to extract inline. Move it later if it gets slow. |
| Tailor a resume with an LLM (M7) | Not built | Yes: `resume.tailoring.requested` → `resume.tailored` | Per-user limit on LLM calls | Calls take seconds, cost money and hit provider limits. The user sees PENDING, then DONE. |
| Auto-submit an application (M9) | Not built | Yes, carefully: `application.submission.requested` | No | It cannot be undone, so never retry blindly. Failures go to a person to review. |
| Job list and job detail reads | Postgres | No | Cache when traffic grows | Many users read the same jobs. Evict the cache on `job.updated`. |
| Login | Postgres + JWT | No | Failed-login counter, logout deny-list | Stops brute-force attacks across all instances. |

## Event flow

_(The interactive event-flow diagram from the original doc does not export to Markdown. Flow: `crawl.requested` → `job.discovered` → `job.created` / `job.updated` → `job.matched` → email; `resume.tailoring.requested` → `resume.tailored`. Redis: crawl lock + rate limit.)_

Each box is a consumer that does one job and can fail and retry on its own. Each arrow is a topic that another box can also subscribe to later, for example an analytics consumer on `job.created`.

## What breaks at scale, and what prevents it

Kafka delivers every message at least once, so the most important habit is making every consumer safe to run twice. Most of the other failures come from that, or from slow outside services.

| Failure | What happens today | Prevention |
| --- | --- | --- |
| Greenhouse is slow or down | The admin request hangs and the whole crawl is lost | Timeout on WebClient. Retry topic with backoff. Dead-letter topic after N tries. |
| The same event arrives twice | Duplicate job rows, or two emails | Idempotent consumers: a unique key in Postgres, or a Redis "processed:{eventId}" marker with TTL |
| One broken message ("poison pill") | Not possible yet | Without a dead-letter topic, the consumer retries it forever and blocks its whole partition |
| Two instances crawl one board | Double API load and racing inserts | Redis lock per board (`SET NX` with expiry) |
| The job board bans us for too many calls | Nothing limits the call rate | Redis rate limit per platform |
| DB save works but the Kafka publish fails | Not possible yet | Transactional outbox: write the event to a table in the same DB transaction, and a relay publishes it |
| Consumers fall behind the producers | Not possible yet | Watch consumer lag. Add partitions and consumers. |
| The LLM provider throttles or fails | Not built | Retry with backoff. The partition count caps concurrency. The user sees PENDING, not an error. |
| Redis goes down | Not used yet | A cache falls back to Postgres. A failed lock means skip this crawl run, never crawl unprotected. |

## Build order

Start with the crawl pipeline. It is the one async problem that already exists in your code, and it teaches every Kafka basic on a single flow.

1. **Crawl pipeline on Kafka.** Covers `crawl.requested` → `job.discovered` → `job.created`. Teaches producers, consumers, message keys and partitions, retries, the dead-letter topic and idempotency.
2. **Redis lock and rate limit for the crawler.** A small step that teaches `SET NX`, TTL and why a lock needs an expiry.
3. **Recommendations and email from events.** Covers `job.created` → `job.matched` → email. Teaches fan-out (several consumers of one topic) and the outbox pattern.
4. **Resume tailoring on Kafka** when you reach M7. Teaches the request → PENDING → DONE status pattern.
5. **Redis cache and login protection, then AWS.** Do these once there is real read traffic and something worth deploying.

You can keep building M6 to M8 the simple way now. Two habits make the later move to Kafka easy: give long jobs a status column (PENDING, DONE, FAILED), and give every write a natural unique key.

First concrete step: add Kafka and Redis to `docker-compose.yml`. Then write down the fields and the key of the `job.discovered` event before writing any code.
