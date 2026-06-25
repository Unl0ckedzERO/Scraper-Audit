# Parse Indeed Test — Rich Compact v3 Refinement Result

Date: 2026-06-25
Zone: Incubator
Tool or Source: Parse `indeed.com` subscribed API variant
Test Type: Refined normalized rich compact extraction + safe extra discovery
Raw Data Stored: No — sanitized summary only.

## Question

Can `search_jobs_rows_rich_compact_v3` improve v2 by cleaning duplicate arrays, adding better relevance scoring/drift flags, and safely checking for additional useful page-level fields outside the current row extraction?

## Setup

Endpoint tested: `search_jobs_rows_rich_compact_v3`

Key inputs:

- query: `heavy equipment operator`
- location: `United States`
- `jt`: `fulltime`
- `fromage`: `14`
- `start`: `0`
- `limit`: `100`
- `maxPages`: `1`
- `dedupe`: `true`
- `includeExtraDiscovery`: `true`

## Results

Sanitized summary:

- Cost: 7 credits.
- `totalJobCount`: 2,210.
- `uniqueJobsCount`: 2,208.
- `rowsReturned`: 59.
- `observedRowsBeforeDedupe`: 59.
- `observedRowsAfterDedupe`: 59.
- `duplicatesRemoved`: 0.
- `detailCallsMade`: 0.
- `externalSearchCallsMade`: 1.
- `fallbackSearchCallsMade`: 0.
- `pagesRequested`: 1.
- `pagesReturned`: 1.
- `arrayValuesDroppedAsCodes`: 830.
- `duplicateArrayValuesRemoved`: 304.

## Improvements Over v2

v3 improved the scoring/readiness layer:

- Requirements were deduped better than v2.
- Relevance scoring fields were added: `relevanceScore`, `relevanceBucket`, `relevanceReason`, `relevancePositiveSignals`, and `relevanceNegativeSignals`.
- Drift flags became materially more useful, catching management/superintendent rows, truck-driver-only rows, low-equipment-signal rows, and likely query drift.
- Some previously weak adjacent roles, such as paver/asphalt-style operator roles, were treated more appropriately as medium when supported by equipment terms.
- Opaque code cleanup remained active.

## Extra Discovery Findings

Extra discovery did not find much additional extraction value beyond the current card payload.

Safe extra findings were limited to small page-level/context signals such as:

- saved job count metadata
- result count text
- estimated available page count

These are useful for pagination/context, but not enough to justify another extraction build. No major missing rich row field was discovered that changes the current stack decision.

## Remaining Issues

v3 is good enough for adoption, but still not perfect:

1. Some benefit/payroll labels can still appear in places that may not be ideal, such as paid biweekly, overtime pay, or similar compensation/schedule labels.
2. Some equipment-adjacent titles remain hard to classify perfectly, such as Gradall Operator, Digger Derrick Operator, or some construction/pipeline roles.
3. Some broad `equipment operator` titles may still be medium or strong even when they are warehouse/recycling/material-handling roles rather than heavy construction equipment.
4. The endpoint remains search-card based, so it still does not provide full descriptions or full apply-page data.

These issues are better handled by downstream sheet scoring or human review than by more endpoint-building.

## Cost Evaluation

- v2: 59 rows / 6 credits ≈ 0.102 credits per row.
- v3: 59 rows / 7 credits ≈ 0.119 credits per row.

v3 costs slightly more in this run but provides better relevance and drift metadata. It should be preferred when ranking quality matters. v2 remains a lower-cost normalized option if scoring fields are not needed.

## Verdict

PASS / Adopt for scoring-ready Parse output.

`search_jobs_rows_rich_compact_v3` is the best current Parse endpoint for rich compact scoring rows.

No further endpoint-building is recommended unless a new use case appears. The remaining value should come from downstream scoring/sheet logic, not more Parse extraction revisions.

## Updated Stack

- ChatGPT Indeed connector: interactive review and application prep.
- Parse `search_jobs_rows_rich_compact_v3`: best scoring-ready compact output.
- Parse `search_jobs_rows_rich_compact_v2`: cleaner normalized rows when scoring metadata is not needed.
- Parse `search_jobs_rows_compact_v3`: lean fallback/job-key discovery.
- Parse `get_job_details`: selective enrichment only.
- Apify Indeed scraper: full rich export and full-description layer.

## Route

The Parse/Indeed Incubator test is closeout-ready.
