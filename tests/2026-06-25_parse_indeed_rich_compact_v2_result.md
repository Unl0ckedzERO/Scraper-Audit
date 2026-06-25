# Parse Indeed Test — Rich Compact v2 Normalization Result

Date: 2026-06-25
Zone: Incubator
Tool or Source: Parse `indeed.com` subscribed API variant
Test Type: Normalized rich compact extraction
Raw Data Stored: No — sanitized summary only.

## Question

Can `search_jobs_rows_rich_compact_v2` normalize the richer v1 card fields into cleaner spreadsheet-ready rows without detail calls?

## Setup

Endpoint tested: `search_jobs_rows_rich_compact_v2`

Key inputs:

- query: `heavy equipment operator`
- location: `United States`
- `jt`: `fulltime`
- `fromage`: `14`
- `start`: `0`
- `limit`: `100`
- `maxPages`: `1`
- `dedupe`: `true`

## Results

Sanitized summary:

- Cost: 6 credits.
- `totalJobCount`: 2,277.
- `uniqueJobsCount`: 2,270.
- `rowsReturned`: 59.
- `observedRowsBeforeDedupe`: 59.
- `observedRowsAfterDedupe`: 59.
- `duplicatesRemoved`: 0.
- `detailCallsMade`: 0.
- `externalSearchCallsMade`: 1.
- `fallbackSearchCallsMade`: 0.
- `pagesRequested`: 1.
- `pagesReturned`: 1.
- `arrayValuesDroppedAsCodes`: 808.

## Evaluation

The v2 normalization pass succeeded.

Compared with v1, v2 preserved the rich compact row value while making the output more spreadsheet-friendly:

- benefits are now readable labels rather than opaque code values
- job type labels are populated
- schedule labels are separated from benefits
- required/preferred requirement labels are separated
- skill/equipment terms are split out from general taxonomy
- equipment term matches are available as relevance helper fields
- title relevance bucket and reason are available per row
- compact rows still come from search-card payload only, with zero detail calls

Cost efficiency improved relative to v1:

- v1: 57 rows / 7 credits ≈ 0.123 credits per row.
- v2: 59 rows / 6 credits ≈ 0.102 credits per row.
- v2 estimated cost: ≈ 102 credits per 1,000 normalized rich compact rows.
- Free 200-credit tier would imply roughly 1,960 normalized rich compact rows/month if this behavior holds.

## Remaining Issues

The endpoint is good enough for adoption as the best Parse row output, but not perfect.

Remaining issues:

1. `requirements` can contain duplicate labels because values appear from multiple requirement sources.
2. `skillEquipmentLabels` sometimes includes non-equipment operational labels such as paid weekly, direct deposit, paid training, overtime pay, and paid biweekly.
3. `driftFlags` did not catch obvious drift rows; many weak rows show empty drift flags.
4. Some title relevance classifications are overly generous, such as warehouse equipment operator being marked strong because the title contains equipment operator.
5. Some relevant adjacent titles are marked weak, such as paver operator and trackhoe-style titles.

These issues can be handled downstream in a sheet/scoring layer or with a small future scoring refinement. They do not block adoption.

## Verdict

PASS / Adopt as best Parse row output.

`search_jobs_rows_rich_compact_v2` should replace lean v3 as the preferred Parse output when the goal is job-search scoring or spreadsheet preview.

Keep lean v3 only for cheap/simple job-key discovery if needed.

Updated stack:

- ChatGPT Indeed connector: interactive review and application prep.
- Parse `search_jobs_rows_rich_compact_v2`: best lightweight normalized scoring rows.
- Parse `search_jobs_rows_compact_v3`: backup/lean compact discovery.
- Parse `get_job_details`: selective enrichment only.
- Apify Indeed scraper: full rich export and full-description layer.

## Route

Testing is now closeout-ready unless the user wants one final scoring-refinement endpoint.
