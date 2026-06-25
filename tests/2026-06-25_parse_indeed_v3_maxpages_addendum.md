# Parse Indeed Addendum — v3 maxPages Test

Date: 2026-06-25
Zone: Incubator
Tool or Source: Parse `indeed.com` subscribed API variant
Test Type: API optimization follow-up
Raw Data Stored: No — sanitized summary only.

## Question

Can `search_jobs_rows_compact_v3` increase compact row yield by changing only `maxPages` from `1` to `2` while keeping the same query and `limit=50`?

## Setup

Same as the successful v3 single-page test, except:

- `maxPages`: `2`

Other key inputs:

- query: `equipment operator`
- location: `Montana`
- `jt`: `fulltime`
- `fromage`: `14`
- `start`: `0`
- `limit`: `50`
- `dedupe`: `true`

## Results

Sanitized summary:

- `rowsReturned`: 53.
- `detailCallsMade`: 0.
- `externalSearchCallsMade`: 3.
- `fallbackSearchCallsMade`: 1.
- `pagesRequested`: 2.
- `pagesReturned`: 1.
- Page 1 at `start=0`: 53 rows found.
- Page 2 at `start=10`: 0 rows found; fallback was used.
- No duplicates were removed.

## Evaluation

The `maxPages=2` test did not improve output. It returned roughly the same row count as the successful single-page v3 test while causing additional upstream search calls and a fallback.

This means the current batching strategy is not useful for cost reduction. The better operating mode remains:

- endpoint: `search_jobs_rows_compact_v3`
- `limit`: `50`
- `maxPages`: `1`

## Verdict

Do not use current `maxPages=2` behavior for cost reduction.

Keep v3 single-page `limit=50` as the compact-preview baseline.

## Next Step

Stop pagination testing unless a revised endpoint can use a cleaner offset/page strategy and avoid fallback waste.
