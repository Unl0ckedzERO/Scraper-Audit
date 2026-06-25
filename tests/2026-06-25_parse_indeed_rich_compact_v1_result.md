# Parse Indeed Test — Rich Compact v1 Result

Date: 2026-06-25
Zone: Incubator
Tool or Source: Parse `indeed.com` subscribed API variant
Test Type: Rich compact extraction / API quality improvement
Raw Data Stored: No — sanitized summary only.

## Question

Can Parse return richer compact Indeed rows from search-card data without calling job detail pages?

## Setup

Endpoint tested: `search_jobs_rows_rich_compact_v1`

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

- Cost: 7 credits.
- `totalJobCount`: 2,272.
- `uniqueJobsCount`: 2,267.
- `rowsReturned`: 57.
- `observedRowsBeforeDedupe`: 57.
- `observedRowsAfterDedupe`: 57.
- `duplicatesRemoved`: 0.
- `detailCallsMade`: 0.
- `externalSearchCallsMade`: 1.
- `fallbackSearchCallsMade`: 0.
- `pagesRequested`: 1.
- `pagesReturned`: 1.

## Field Quality Observed

The endpoint successfully returned materially richer compact rows than `search_jobs_rows_compact_v3`.

Useful fields now present include:

- structured salary text and min/max/type/currency
- normalized title and display title
- city/state/postal/location count
- additional-location label
- posted age plus timestamp fields
- company rating and review count
- employer responsiveness fields
- apply flags and resume requirement type
- urgent/high-volume/hiring event flags
- hires-needed fields
- remote and sponsored flags
- package tier
- requirements and requirement strictness
- screener requirements
- taxonomy labels
- taxo attributes
- benefits-like fields
- snippet and generated Indeed job URL

## Issues / Cleanup Needed

The endpoint is successful, but v1 needs a cleanup pass before adoption as a stable workflow output.

Observed issues:

1. `benefits` currently includes opaque code-like values rather than clean user-facing benefit labels.
2. `taxonomyLabels` mixes job type labels with benefit labels and schedule labels.
3. `jobTypeLabels` appears empty even though job type data exists in taxonomy labels.
4. `taxoAttributes` sometimes mixes readable labels and internal codes.
5. Some relevance drift remains, including construction superintendent, construction supervisor, truck-driver-heavy listings, food packaging equipment, and similar adjacent roles.
6. `excludedUnsafeFieldCount` reported 0, which may mean excluded fields were omitted before counting rather than that none existed.

## Cost Evaluation

Cost efficiency:

- 7 credits / 57 rich compact rows ≈ 0.123 credits per row.
- ≈ 123 credits per 1,000 rich compact rows.
- 200 free credits/month would imply about 1,625 rich compact rows/month if this behavior holds.

This is slightly less efficient than the lean compact v3 endpoint but provides much more useful scoring data.

## Verdict

PASS as proof of concept.

`search_jobs_rows_rich_compact_v1` proves Parse can become a useful rich compact scoring layer, not just a snippet extractor.

Do not treat v1 as final. A v2 cleanup endpoint should normalize arrays and remove opaque codes before this becomes the default sheet output.

## Recommended v2 Cleanup

A follow-up endpoint should:

- keep salary, company rating/review count, posting dates, apply flags, urgent/hiring flags, requirements, and location fields
- split taxonomy into clean output fields:
  - `jobTypeLabels`
  - `scheduleLabels`
  - `benefitLabels`
  - `requirementLabels`
  - `skillEquipmentLabels`
- remove opaque SUID/code values from `benefits`, `taxoAttributes`, and taxonomy fields
- avoid duplicate benefit labels
- preserve only readable strings
- optionally add simple relevance flags/counts based on title, normTitle, requirements, taxo attributes, and snippet

## Route

Keep Parse as:

- compact/rich-preview scoring layer
- query testing layer
- job-key discovery layer

Keep Apify as:

- full/rich export layer
- full description and broader field export path

Keep Indeed connector as:

- interactive review and application-prep layer
