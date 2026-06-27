# Handoff — Parse / Indeed API Tool Stack for Job Search

Date: 2026-06-27
Source Zone: Incubator
Target Zone: Job Search
Item Type: Tool Stack / API / Scraper / Data Source
Status: Adopted for Job Search use, Incubator closed for now

## Why This Passed Incubator

- The Incubator test clarified that no single source should own all Indeed job-search extraction.
- Parse improved from a weak marketplace baseline into a useful compact row extraction layer after endpoint refinement.
- Apify remains the stronger paid rich-export layer when larger structured datasets are justified.
- The ChatGPT Indeed connector remains useful for low-cost interactive review and initial exploration.
- The final workflow is a layered tool stack that balances cost, field richness, speed, and cleanup burden.

## What Is Known

- Parse marketplace `search_jobs` was useful for search-state data, counts, related queries, pagination, and job keys, but not clean enough for direct sheet population by itself.
- Parse `get_job_details` is useful only for selected high-value job keys because detail-calling every result is too expensive for broad extraction.
- Parse refined row endpoints can return compact, scoring-ready search rows.
- The best current Parse endpoint style is `search_jobs_rows_rich_compact_v3` for compact, table/scoring-friendly rows.
- Apify `borderline/indeed-scraper` remains the preferred paid full-rich-export layer when deeper structured output is justified.
- The Indeed connector remains the default low-friction interactive review tool, but should not be treated as exhaustive when broad state/national sweeps matter.

## Adopted Job Search Tool Stack

| Job Search Need | Preferred Source | Notes |
|---|---|---|
| Quick interactive review | ChatGPT Indeed connector | Use first when a small visible set is enough. |
| Compact scoring-ready rows | Parse `search_jobs_rows_rich_compact_v3` style endpoint | Use when row data is needed but full rich export is not justified. |
| Search-state probe / fallback | Parse marketplace search or earlier Parse row endpoints | Use when compact endpoint fails or for market-size/search-term discovery. |
| Selected detail enrichment | Parse detail endpoint | Use only for chosen high-priority jobs. |
| Paid rich export | Apify `borderline/indeed-scraper` | Use for larger/richer datasets when cost is justified. |

## Recommended Use Order

1. Start with the Indeed connector for quick review and visible leads.
2. Use Parse rich compact rows when a scoring-ready table slice is needed.
3. Use selective Parse details only for jobs worth extra enrichment.
4. Use Apify when the search lane needs a fuller paid export or broader structured dataset.
5. Summarize and sanitize results before logging anything in The Lab repo.

## What Is Unknown / Watch Items

- Whether Parse pricing, public-fork behavior, or revision costs change.
- Whether Indeed changes page structure or blocks/fails one of the endpoint methods.
- Whether the rich compact endpoint remains stable across broader queries.
- Whether Apify pricing or actor output shape changes.
- Whether the connector expands or limits visible result sets in future.

## Routing After Adoption

- Normal job-search usage: Job Search project.
- New endpoint refinement or Parse platform behavior change: Indeed API Incubator can be reopened.
- New scraper comparison or pricing change: Incubator.
- Durable routing/naming/index changes: Framework.
- Raw job listings or application decisions: Job Search, not The Lab Framework.

## Source Files

- `tests/2026-06-27_parse_indeed_api_incubator_closeout.md`
- `tests/2026-05-26_parse_indeed_pipeline_assessment.md`
- `tests/2026-05-26_parse_indeed_montana_search_and_revision_hypothesis.md`
- `tests/2026-05-26_apify_borderline_indeed_results_evaluation.md`
- `tests/2026-06-14_apify_indeed_paid_export_layer_evaluation.md`
- `handoffs/2026-06-13_archive_to_incubator_parse_indeed_search_table_experiment.md`

## Sanitization Notes

Do not commit raw job datasets, raw Parse responses, raw Apify exports, API keys, credentials, signed/private links, account-specific metadata, or unredacted API responses. The Lab repo should keep only sanitized summaries, decisions, handoffs, and workflow standards.
