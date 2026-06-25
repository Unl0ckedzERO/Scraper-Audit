# Parse Indeed Addendum — v3 Limit 100 Test

Date: 2026-06-25
Zone: Incubator
Tool or Source: Parse `indeed.com` subscribed API variant
Test Type: API optimization follow-up
Raw Data Stored: No — sanitized summary only.

## Question

Does increasing `limit` from `50` to `100` improve compact row yield for `search_jobs_rows_compact_v3` while keeping `maxPages=1`?

## Setup

Same as the successful v3 single-page test, except:

- `limit`: `100`
- `maxPages`: `1`

Other key inputs:

- query: `equipment operator`
- location: `Montana`
- `jt`: `fulltime`
- `fromage`: `14`
- `start`: `0`
- `dedupe`: `true`

User also reported that the previous `maxPages=2` test cost 9 credits.

## Results

Sanitized `limit=100` summary:

- Cost: 6 credits.
- `rowsReturned`: 54.
- `totalJobCount`: 55.
- `uniqueJobsCount`: 54.
- `observedRowsBeforeDedupe`: 54.
- `observedRowsAfterDedupe`: 54.
- `observedRowsAfterFiltering`: 54.
- `duplicatesRemoved`: 0.
- `detailCallsMade`: 0.
- `externalSearchCallsMade`: 1.
- `fallbackSearchCallsMade`: 0.
- `pagesRequested`: 1.
- `pagesReturned`: 1.
- `requestedLimit`: 100.
- `limitAppearsHonored`: true.

## Evaluation

Increasing `limit` from `50` to `100` did not materially improve yield. The earlier v3 single-page `limit=50` test returned 55 rows for 6 credits; this `limit=100` test returned 54 rows for the same 6 credits.

This suggests the practical ceiling for this query is around the unique available result count, not the requested limit value. For this query, both `limit=50` and `limit=100` appear to pull essentially the full available compact search-card set in one request.

The separate `maxPages=2` result cost 9 credits and did not add useful rows, so batching is worse than single-page extraction for this query.

## Verdict

Keep the operating baseline as:

- endpoint: `search_jobs_rows_compact_v3`
- `limit`: `50` or `100`
- `maxPages`: `1`
- `dedupe`: `true`

Prefer `limit=50` as the default because it already reached the same practical yield at the same cost in the earlier test. Use `limit=100` only as an occasional ceiling probe for query types with more than ~50 available results.

## Next Step

Stop limit/pagination optimization for this query. Future useful tests should check whether v3 single-page behavior holds on different query/location patterns, or whether filtering improves relevant-row quality.
