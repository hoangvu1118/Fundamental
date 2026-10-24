# Pagination study guide (closing Milestone 5)

Read against `main` @ `9f058a5` on 2026-10-10. Concepts first, then how Spring does it, then the two
endpoints. Each section ends with questions. Answer them in the thread before you write code.

## 1. Why paginate at all?

Today `GET /api/v1/job` calls `jobRepository.findAll(spec, sort)` (`JobService.java:46`) and returns every
open job. Think through what happens when the table holds 50 jobs, then 50,000:
- the database reads and sends every row
- Hibernate builds 50,000 `Job` objects (with `description`, a big text column, even though the summary DTO never shows it)
- Jackson writes a multi-MB JSON body, and the client renders it
- the heap of one request grows with table size, so a few concurrent users can push the JVM over

**Questions**
1. Which of those costs is paid by the DB, which by your JVM, which by the network? Which one breaks first?
2. A UI shows 20 cards. Why should the server, not the client, decide how many rows leave the DB?

## 2. The two families: offset vs keyset (cursor)

**Offset**: `ORDER BY created_date DESC LIMIT 20 OFFSET 40` ("page 3").
- Simple, lets you jump to any page, pairs naturally with "page 3 of 17".
- The DB still walks and throws away the first 40 rows, so deep pages get slower.
- Unstable under writes: if a new job is inserted while the user is on page 1, page 2 repeats a row.
  If one is deleted, a row is skipped.

**Keyset / cursor**: `WHERE (created_date, id) < (:lastDate, :lastId) ORDER BY created_date DESC, id DESC LIMIT 20`.
- Every page costs the same (index seek), stable under inserts/deletes.
- No "jump to page 9", no total count; the client gets an opaque "next" cursor.
- Needs a unique, indexed sort key; sorting by an arbitrary column the user picks gets hard.

**Questions**
3. Why does the sort key need a tie breaker like `id`? What goes wrong with `ORDER BY match_score DESC`
   alone when 30 recommendations all score 60? (Hint: SQL gives no ordering guarantee among ties.)
4. For `/job-recommendations`: a user dismisses a job on page 1, then loads page 2. With offset, what
   happens to the row that was first on page 2? With keyset?
5. Which UX does each endpoint want: numbered pages, or "load more" / infinite scroll? Let that drive the choice.

## 3. The hidden cost: counting

"Page 3 of 17" needs `SELECT count(*)` with the same WHERE clause, run on every request. On Postgres,
`count(*)` over many rows is not free (MVCC, no cached row count).

**Questions**
6. Does your client actually need `totalElements`/`totalPages`, or just `hasNext`?
7. How could you know `hasNext` without a count? (Hint: what if you ask for `size + 1` rows?)

## 4. What Spring Data gives you

Look these up in the Spring Data JPA reference (Boot 4.1 ships Spring Data 4.x):

| Type | Runs a count? | Gives you |
|---|---|---|
| `Pageable` / `PageRequest.of(page, size, sort)` | n/a | the request: page index (0-based), size, `Sort` |
| `Page<T>` | yes | content + total elements/pages |
| `Slice<T>` | no (fetches size+1) | content + `hasNext` |
| `Window<T>` + `ScrollPosition` (`OffsetScrollPosition` / `KeysetScrollPosition`) | no | scrolling API, keyset support built in |

Things to try or read about:
- A repository method can take a `Pageable` and return `Page`, `Slice` or `List`. Derived queries
  (`findBySearchProfileIdAndStatusNot(..., Pageable)`) and `JpaSpecificationExecutor.findAll(spec, pageable)` both work.
- With `Page`, Spring derives the count query for you. With a custom `@Query` you can supply `countQuery`. Why might you want to?
- Controllers can take `Pageable` directly: `?page=0&size=20&sort=createdDate,desc` is bound by
  `PageableHandlerMethodArgumentResolver`. Look at `spring.data.web.pageable.*` properties
  (`max-page-size`, `default-page-size`, `one-indexed-parameters`).
- Returning a raw `Page<T>` from a controller logs a warning in recent Spring Data: its JSON shape is not
  a stable contract. Read about `@EnableSpringDataWebSupport(pageSerializationMode = VIA_DTO)` / `PagedModel`,
  and compare with your planned `PageResponse<T>`.

**Questions**
8. If `Pageable` comes straight from the request, a user can send `size=100000` or `sort=searchProfile.user.passwordHash`.
   What protects you from each? Should the client be allowed to choose the sort for recommendations at all?
9. `PageResponse<T>` of your own vs `PagedModel` vs raw `Page`: what does each couple your API to?

## 5. Pagination meets JPA fetching (the gotcha for this milestone)

`JobRecommendation` has a `@ManyToOne` `job` (lazy) and an `@ElementCollection` `matchReasons`.
- Fetching a **to-one** association with `@EntityGraph` or `JOIN FETCH` plus a page: works, still one row per recommendation, `LIMIT` is applied in SQL.
- Fetching a **collection** (`matchReasons`) with `JOIN FETCH` plus a page: each recommendation becomes
  several rows, so SQL `LIMIT 20` would cut a recommendation's reasons in half. Hibernate notices and
  instead loads **everything** and paginates in memory (look for warning `HHH90003004` /
  "firstResult/maxResults specified with collection fetch; applying in memory").

**Questions**
10. So how do you get 20 recommendations, each with its job and all its reasons, in a bounded number of
    queries? Compare: (a) page over IDs first, then fetch by `id IN (...)`; (b) fetch the page with job only and
    let `@BatchSize` / `hibernate.default_batch_fetch_size` load reasons in one extra query; (c) a DTO projection.
11. How many SQL statements does your current plan issue per page? Turn on `spring.jpa.show-sql` (or
    `logging.level.org.hibernate.SQL=debug`) and count them. Include the count query.

## 6. Applying it to SeFuJo

### `GET /job-recommendations` (new)
Agreed so far: scoped to the caller's profile, exclude `DISMISSED`, sort `matchScore desc, id desc`, cap size, job loaded in the same query.
Open for you to decide and justify:
- `Page` or `Slice`? Offset or keyset? (Question 4 and 6 should decide this.)
- Which index makes this fast? Write the `WHERE` + `ORDER BY` out and design the index in a new migration.
- Should recommendations for `CLOSED` jobs be hidden here?
- `JobRecommendationResponse` still holds the `Job` entity and a single `MatchReason`
  (`JobRecommendationResponse.java:16-17`). What should it hold so serialization never touches a lazy proxy?

### `GET /api/v1/job` (existing)
- The repository already overrides `findAll(spec, sort)` with `@EntityGraph("company")`
  (`JobRepository.java:19-23`). Does that override also apply to `findAll(spec, pageable)`? Check the
  SQL log rather than assuming.
- Sorting by `createdDate` desc: is `createdDate` unique? What is your tie breaker?
- Users filter by title/location here. Does that change whether keyset is practical?

## Suggested order
1. Answer questions 1 to 9 in the thread (short answers are fine).
2. Build `PageResponse<T>` and decide its fields.
3. Page `/job-recommendations` with SQL logging on; answer 10 and 11 from what you see.
4. Page `/jobs`; check the company fetch and the count query in the log.
5. Push and ask for a review.
