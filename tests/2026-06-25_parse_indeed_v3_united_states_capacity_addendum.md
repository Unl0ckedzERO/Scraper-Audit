# Parse Indeed Addendum — v3 United States Capacity Test

Date: 2026-06-25
Zone: Incubator
Tool or Source: Parse `indeed.com` subscribed API variant
Test Type: API optimization follow-up
Raw Data Stored: No — sanitized summary only.

## Question

Can `search_jobs_rows_compact_v3` return materially more than ~55 compact rows when the result pool is much larger?

## Setup

Same as the successful v3 single-page test, but location was broadened from `Montana` to `United States`.

Key inputs:

- query: `equipment operator`
- location: `United States`
- `jt`: `fulltime`
- `fromage`: `14`
- `start`: `0`
- `limit`: `100`
- `maxPages`: `1`
- `dedupe`: `true`

## Results

Sanitized summary:

- Cost: 7 credits.
- `totalJobCount`: 9,220.
- `uniqueJobsCount`: 6,429.
- `rowsReturned`: 59.
- `observedRowsBeforeDedupe`: 59.
- `observedRowsAfterDedupe`: 59.
- `observedRowsAfterFiltering`: 59.
- `duplicatesRemoved`: 0.
- `detailCallsMade`: 0.
- `externalSearchCallsMade`: 1.
- `fallbackSearchCallsMade`: 0.
- `pagesRequested`: 1.
- `pagesReturned`: 1.
- `requestedLimit`: 100.
- `limitAppearsHonored`: true.

## Evaluation

The broader `United States` location proved that the underlying result pool can be very large, but the compact search-card payload still returned only about 59 rows in a single v3 call.

This suggests a practical single-call compact-row ceiling around ~55–60 rows for this query pattern, even when thousands of results are available.

Cost efficiency remained good:

- 7 credits / 59 rows ≈ 0.119 credits per compact row.
- ≈ 119 credits per 1,000 compact rows.
- 200 free credits/month would imply roughly 1,680 compact rows/month if this behavior holds.

However, broadening to the national level increased relevance drift. Returned rows included heavy equipment roles, but also machine operators, truck drivers, delivery drivers, CNC roles, production operators, and other looser matches.

## Verdict

`search_jobs_rows_compact_v3` remains useful as a compact preview layer, but the single-call ceiling appears to be around ~55–60 rows rather than 100 rows.

For broad/national searches, relevance filtering or more specific queries matter more than increasing `limit` or `maxPages`.

## Next Step

Test a more specific national query such as `heavy equipment operator` with v3 single-page settings to see whether relevance improves while preserving the ~55–60 row yield.
