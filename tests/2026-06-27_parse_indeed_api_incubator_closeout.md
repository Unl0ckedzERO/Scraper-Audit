# Parse / Indeed API Incubator Closeout — Job Search Tool Stack

Date: 2026-06-27
Zone: Incubator
Tool or Source: Parse Indeed API fork, Apify Indeed scraper, ChatGPT Indeed connector
Test Type: API / Scraper / Workflow / Job Search Data Source
Raw Data Stored: No — only sanitized summary and evaluation are committed.

## Question

Can the Parse Indeed API, Apify Indeed scraper, and ChatGPT Indeed connector be combined into a practical Job Search tool stack for finding, enriching, and exporting job leads without overpaying for unnecessary detail calls?

## Setup

- Baseline: ChatGPT Indeed connector for interactive review and visible result inspection.
- Paid export comparison: Apify `borderline/indeed-scraper` for structured row-level exports.
- Parse marketplace baseline: `search_jobs` and `get_job_details`.
- Parse fork/refinement path: custom row-returning search endpoints, ending with the `search_jobs_rows_rich_compact_v3` style output.
- Cost constraint: use free/monthly Parse credits carefully; use Apify only when a paid export is justified.
- Sanitization constraint: do not commit raw API responses, job datasets, signed links, credentials, or private account metadata.

## Prior Indexed Evidence

Relevant prior files:

- `tests/2026-05-26_parse_indeed_pipeline_assessment.md`
- `tests/2026-05-26_parse_indeed_montana_search_and_revision_hypothesis.md`
- `tests/2026-05-26_apify_borderline_indeed_results_evaluation.md`
- `tests/2026-06-14_apify_indeed_paid_export_layer_evaluation.md`
- `handoffs/2026-06-13_archive_to_incubator_parse_indeed_search_table_experiment.md`

## Sanitized Observations

- Parse marketplace `search_jobs` was useful for search-state data, counts, related queries, pagination/context, and job keys, but not sufficient as a clean sheet-ready row extractor by itself.
- Parse marketplace `get_job_details` returned richer detail for a specific job key, but detail-calling every result is too expensive for broad sweeps.
- Parse fork revisions improved row readiness and produced compact row-style search outputs suitable for scoring and review.
- The best Parse role after refinement is a lightweight scoring-ready search-row probe, not a full replacement for every downstream source.
- Apify remains the stronger choice when a full rich export is justified, especially for larger or more complete structured datasets.
- The Indeed connector remains useful for interactive review because it is convenient and does not add an external scraping bill, but it may expose only a limited visible slice at a time.
- The practical result is a layered tool stack rather than a single winner.

## Adopted Tool Stack

| Layer | Preferred Tool | Role |
|---|---|---|
| Interactive review | ChatGPT Indeed connector | Fast review, visible lead inspection, initial exploration. |
| Scoring-ready compact rows | Parse `search_jobs_rows_rich_compact_v3` style endpoint | Cheap/controlled search-row extraction when compact fields are enough. |
| Parse fallback | Earlier Parse row endpoints / marketplace search | Use only if rich compact endpoint fails or a narrower search-state probe is needed. |
| Selective detail enrichment | Parse detail endpoint | Use only for selected high-value job keys, not broad detail sweeps. |
| Full rich export | Apify `borderline/indeed-scraper` | Use when a larger, richer, paid structured dataset is justified. |

## Evaluation

What worked:

- The Incubator test found a clearer role for Parse after refinement: compact, scoring-ready search rows.
- Apify's role stayed clear: paid bulk/rich export layer.
- The Indeed connector remains useful for low-friction interactive review.
- The final decision avoids forcing all job-search work through the most expensive or heaviest source.

Remaining cautions:

- Parse endpoint behavior and pricing may change.
- Parse revisions may consume credits unless the platform/public-fork path changes.
- Apify cost is predictable enough for controlled export use, but should still be used intentionally.
- Connector visibility limitations mean it should not be treated as proof that no more jobs exist.
- Any raw job exports or API responses should remain outside the repo unless sanitized and summarized.

## Verdict

Tool Stack / Existing Project Handoff.

Close the Indeed API Incubator for now. Treat the result as a Job Search data-source/tool-stack decision, not an active ongoing Lab experiment.

## Route

- Job Search should use the adopted layered tool stack when job-search evidence extraction is needed.
- Framework should keep the routing rule and manifest index current.
- Reopen Incubator only for significant Indeed, Parse, Apify, pricing, endpoint, connector, or output-shape changes.

## Next Step

Use the handoff file `handoffs/2026-06-27_incubator_to_job_search_parse_indeed_api_tool_stack.md` as the Job Search-facing summary.

## Sanitization Notes

Do not commit raw datasets, raw Parse responses, raw Apify exports, API keys, credentials, signed/private links, unredacted job datasets, or sensitive metadata. Commit only sanitized summaries, workflow decisions, handoffs, and reusable routing rules.
