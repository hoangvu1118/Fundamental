# Milestone 5 review: Recommendation Engine (2026-10-05)

Reviewed commit `62f7c5d` ("feat: job recommendation based on user profile") against roadmap §12.
No code was changed. Every point below is something for you to verify and decide on.

**Definition of done:** "An authenticated user can see a ranked list of jobs based on their SearchProfile."

## Where you stand

| Roadmap task | State |
|---|---|
| Create `JobRecommendation` | Entity exists, but it does not match its migration (see 1) |
| Build scoring service | Done: `RuleBasedJobMatchingStrategy`, behind a `JobMatchingStrategy` interface |
| Generate recommendations | Done, but only inside a POST request (see 5) |
| Store `match_score` | Done |
| Store `match_reasons` | Entity uses a collection table that no migration creates |
| Support statuses | Enum exists, nothing can change it |
| `GET /job-recommendations` | Missing |
| `PATCH /job-recommendations/{id}` | Missing (`UpdateRecommendationStatusRequest` is unused) |
| Ranked list | Missing: nothing sorts by score |

Good choices worth keeping: the split into candidate retrieval (`JobCandidateService`, SQL filter) and
scoring (`JobMatchingStrategy`, in Java) is the right shape, and the interface makes an embeddings or
LLM strategy pluggable later. Upserting on `(search_profile, job)` so a re-run keeps the user's status is
also the right instinct.

## Bugs and gaps (most serious first)

### 1. The schema probably isn't what you think it is
- `V8_update_Jobdescription_type.sql` and `V9_create_job_recommendation.sql` use one underscore.
  Flyway needs `V9__`, so recent Flyway versions skip these files without an error.
  Question: what does `SELECT version, description FROM flyway_schema_history;` show on your local DB?
  If `job_recommendation` exists anyway, how did it get there (the commented-out `ddl-auto=create`)?
  What happens on a fresh database, or in CI, or on AWS later?
- Even if V9 ran, the entity disagrees with it:
  - `JobRecommendation.java:45` maps `update_at`, the table has `updated_at`.
  - `JobRecommendation.java:31-38` expects a `job_recommendation_match_reasons` table; the migration
    instead has an unused `match_reason VARCHAR(1000)` column.
  - `JobRecommendation.java:40` `status` has no `@Enumerated(EnumType.STRING)`, so Hibernate stores an
    ordinal integer into a VARCHAR column. Its DB default is `'ACTIVE'`, which isn't a `RecommendationStatus`.
  - No foreign keys on `job_id` / `search_profile_id`. What should happen to recommendations when a profile is deleted?
  With `ddl-auto=validate` some of this should stop the app from starting. Does it start for you, and why?

### 2. The API returns the JPA entity
`JobRecommendationResponse.java:10` holds `List<JobRecommendation>`, which has lazy `Job` and
`SearchProfile` -> `User` (with `password_hash`). Jackson will either throw on the Hibernate proxy or
serialize far more than you want. Every other module of yours uses DTOs; why not this one?
Also: `@Data` on entities with relations gives you `equals/hashCode/toString` that walk lazy associations.

### 3. The score doesn't discriminate much
- `DatabaseJobCandidateService.java:39-45` already filters candidates by location, so
  `LOCATION_MATCH` (+20) fires for every candidate when the profile has locations. With the cut-off at
  `>= 20` (`JobRecommendationService.java:58`), every candidate passes. What does the threshold actually filter?
- Ingestion never sets `employmentType` or `workplaceType` (only `JobPostingPersistenceService.java:73-76`
  touches title/status), so `EMPLOYMENT_TYPE_MATCH` can never fire and the real max is 80, not 100.
  This is also why you had to comment out the filters at `DatabaseJobCandidateService.java:24-37`.
  That's a Milestone 4 normalization gap leaking into Milestone 5.
- `RuleBasedJobMatchingStrategy.java:32` `title.contains(jobTitle)`: what if a job's normalized title is
  short ("engineer") or empty? `"x".contains("")` is true.
- Substring matching: does skill "go" match "good communication"? Does "java" match "javascript"?
- Roadmap says "keyword overlap"; the profile has no excluded keywords, so you can't say "no PHP".
- `level` exists on SearchProfile and `experience_level` on Job, but scoring ignores both. For an
  internship hunter, isn't level the most important signal?

### 4. Ranking and lifecycle
- Nothing sorts by `match_score`, so the list isn't ranked: the definition of done isn't met yet.
- A `DISMISSED` job keeps coming back on the next POST. Should it?
- If a job closes, its recommendation stays. Should `GET` hide recommendations for closed jobs?

### 5. Generating inside the request
`POST /api/v1/jobRecommendation` computes over every candidate synchronously, with a
`findBySearchProfileAndJob` + `save` per job (N+1 round trips) and no `@Transactional`
(a failure halfway leaves half the rows written). Fine for 50 jobs. What about 50,000 jobs and 1,000 users?
Also: generation is triggered by the user, not by new jobs arriving. Who should trigger it?
This is exactly the "natural asynchronous boundary" roadmap §17 says Kafka needs later, so it's worth
thinking about now even if you don't build it now.

### 6. Outside the milestone but real
- `SecurityConfig.java:37` protects `/admin/**`, but the ingestion route is `/api/v1/admin/ingestion`
  (`JobIngestionController.java:14`). The matcher doesn't match, so any logged-in user can trigger crawls.
- `SearchProfileService.java:80` throws "User not found" when the *profile* is missing.
- REST naming: roadmap says `/job-recommendations`; code has `/jobRecommendation` (camelCase, singular).
- Tests: only `SeFuJoApplicationTests.java`. The scoring strategy is a pure function: the easiest
  thing in the whole codebase to unit test.

## Options for what to tackle next

**A. Close Milestone 5 properly (recommended).**
Fix the migrations and entity mapping, add DTOs, add `GET` (sorted, paged, excluding dismissed) and
`PATCH` for status, and write unit tests for the scoring rules.
Pro: meets the definition of done; small and testable; everything later (resume tailoring needs
`READY_TO_APPLY`, Kafka needs a stable recommendation model) builds on it.
Con: less exciting; scoring stays naive for now.

**B. Improve match quality first.**
Make ingestion fill employment type, workplace type and level, then re-enable the filters and rethink
weights and threshold.
Pro: recommendations become actually useful for you as a user.
Con: it's mostly Milestone 4 debt; tuning weights without tests and a working GET is guesswork.

**C. Move generation out of the request now.**
Scheduled ingestion, then "new jobs ingested -> score them against all active profiles", with GET only reading.
Pro: the real scalability fix, and a natural lead-in to Kafka (and later Redis for caching ranked lists).
Con: jumps ahead of the roadmap; building async plumbing on a schema that may not migrate is backwards.

**Recommendation:** A, then B, then C. A is what the roadmap's definition of done asks for. Do the
security matcher fix along the way since it's one line. Keep C in mind while doing A: if `GET` only
*reads* stored recommendations, then moving generation async later doesn't change your API at all.

## Questions to think about before coding
1. Should `GET /job-recommendations` compute anything, or only read rows that something else wrote?
2. When a user edits their search profile, what happens to existing recommendations and their statuses?
3. Which matches should be hard filters (SQL) and which should be soft signals (score)? Is location really a hard filter for a remote job?
4. How would you write a test proving "a user can't PATCH another user's recommendation"?
5. If two requests generate recommendations for the same profile at once, what does the unique constraint do to the second one?
