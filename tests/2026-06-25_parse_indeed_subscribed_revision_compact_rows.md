# Parse Indeed Test — Subscribed Revision and Compact Search Rows

Date: 2026-06-25
Zone: Incubator
Tool or Source: Parse `indeed.com` API, subscribed/public variant; Apify `borderline/indeed-scraper` comparison
Test Type: API / Platform Workflow / Cost Comparison
Raw Data Stored: No — only sanitized summary and evaluation are committed.

## Question

Did the Parse `Subscribe` path allow free revisions to the public/subscribed `indeed.com` API variant, and can a revised endpoint return compact Indeed search-result rows without per-job detail calls?

Secondary question: does free revision support make Parse useful for cost/yield optimization against Apify?

## Setup

- Parse free plan: 200 monthly credits.
- Apify free plan: $5 monthly free usage credit.
- Earlier Parse result: public `search_jobs` v5 returned page-state/search metadata rather than sheet-ready rows.
- A previous revision submitted while an old private fork existed attached to the private fork and consumed credits during build/testing.
- Support clarified: clicking `Subscribe` is the public fork path.
- User deleted earlier Indeed API subscriptions/forks, resubscribed, and confirmed the revision bar appeared on the new subscribed variant.

Controlled revision test:

1. Add static `ping_parse_revision_test` endpoint to subscribed variant.
2. Confirm whether credits changed.
3. Confirm whether private fork was untouched.
4. Add `search_jobs_rows_compact` endpoint to subscribed variant.
5. Run typical test query:
   - query: `equipment operator`
   - location: `Montana`
   - `jt`: `fulltime`
   - `fromage`: `14`
   - `start`: `0`

Optimization follow-up:

- Add `search_jobs_rows_compact_v2` to test whether a larger `limit` improves rows per runtime call.
- Add `search_jobs_rows_compact_v3` to reduce duplicate upstream calls and preserve high row yield.
- Typical optimization query:
  - query: `equipment operator`
  - location: `Montana`
  - `jt`: `fulltime`
  - `fromage`: `14`
  - `start`: `0`
  - `limit`: `50`
  - `maxPages`: `1`
  - `dedupe`: `true`

## Results

### Revision routing / billing

- Static endpoint revision succeeded.
- Credits did not change.
- New endpoint appeared on the subscribed API variant.
- Private fork was unchanged.
- `search_jobs_rows_compact`, `search_jobs_rows_compact_v2`, and `search_jobs_rows_compact_v3` revisions succeeded and were free.

Interpretation:

- `Subscribe` is Parse's public/subscribed fork path.
- The revision bar is safe when used from the subscribed variant.
- Existing private forks can confuse routing; verify the target variant before revising.
- Revision/build can be free, but endpoint execution still costs credits.

### Compact-row endpoint output

The subscribed `search_jobs_rows_compact` test cost 6 credits and returned compact search-card rows.

Sanitized output summary:

- `totalJobCount`: 56
- `uniqueJobsCount`: 55
- `rowsReturned`: 23
- `jobKeysFound`: 23
- `detailCallsMade`: 0
- `extractionMode`: `search_page_only`
- Useful paths reported:
  - `mosaic-provider-jobcards`
  - `spa.body`
  - `relatedQueries`
  - `totalJobCount`
  - `uniqueJobCount`
  - `metaData.mosaicProviderJobCardsModel.results`

Returned compact fields included:

| Field | Result | Notes |
|---|---|---|
| `jobkey` | Present | Useful for dedupe and selective enrichment. |
| `title` | Present | Search-card title. |
| `company` | Present | Search-card employer. |
| `location` | Present | Search-card location string. |
| `salary` | Partial | Present when Indeed search card exposes it. |
| `snippet` | Present | Search-card snippet, not full job description. |
| `postedAge` | Present | Relative posting age. |
| `jobUrl` | Present | Indeed viewjob URL built from job key. |
| `source` | Present | `Indeed`. |
| Full description | Missing | Requires richer scrape/detail layer. |
| Apply URL | Missing | Use Apify or detail endpoint when needed. |
| Benefits / attributes / requirements / occupation tags | Missing | Use Apify when needed. |

### Optimization output

`search_jobs_rows_compact_v2` tested `limit=50` and returned a much higher row yield.

Sanitized v2 summary:

- Cost: 7 credits.
- `rowsReturned`: 53.
- `detailCallsMade`: 0.
- `extractionMode`: `search_page_only`.
- `externalSearchCallsMade`: 2.
- Result: High yield, but possibly over-fetched because it made two upstream search calls.

`search_jobs_rows_compact_v3` was revised to avoid duplicate upstream requests for `maxPages=1`.

Sanitized v3 summary:

- Cost: 6 credits.
- `rowsReturned`: 55.
- `observedRowsBeforeDedupe`: 55.
- `observedRowsAfterDedupe`: 55.
- `observedRowsAfterFiltering`: 55.
- `duplicatesRemoved`: 0.
- `detailCallsMade`: 0.
- `externalSearchCallsMade`: 1.
- `fallbackSearchCallsMade`: 0.
- `pagesRequested`: 1.
- `pagesReturned`: 1.
- `requestedLimit`: 50.
- `limitAppearsHonored`: false.
- Result: Strongest compact-row result. High yield was preserved while reducing upstream search calls to one.

Interpretation:

- `limit=50` materially improves compact row yield even though Parse reported `limitAppearsHonored: false`.
- The practical result is that the underlying search/card payload exposed ~55 rows in one runtime call.
- v3 should replace v1/v2 for compact preview use.

### Cost estimate

Observed Parse compact-row tests around this endpoint:

| Test | Credits | Rows | Credits / row | Credits / 1,000 rows |
|---|---:|---:|---:|---:|
| Private-fork compact page 1 | 5 | 23 | 0.217 | 217 |
| Private-fork compact page 2 | 6 | 15 | 0.400 | 400 |
| Private-fork `loader operator` | 6 | 24 | 0.250 | 250 |
| Subscribed compact typical test | 6 | 23 | 0.261 | 261 |
| Compact v2, `limit=50` | 7 | 53 | 0.132 | 132 |
| Compact v3, `limit=50` | 6 | 55 | 0.109 | 109 |

Updated estimate:

- Earlier compact estimate: ~0.261–0.274 credits/job, or ~261–274 credits per 1,000 compact rows.
- Optimized v3 estimate: ~0.109 credits/job, or ~109 credits per 1,000 compact rows.

Parse free-tier implication:

- 200 free credits/month ÷ ~0.109 credits/job ≈ ~1,830 compact rows/month if v3 behavior holds.

Parse paid Hobby implication:

- $30/month for 1,000 credits = $0.03/credit.
- 109 credits/1,000 compact rows × $0.03 ≈ $3.27 per 1,000 compact rows.

Apify comparison:

- Apify `borderline/indeed-scraper` verified pricing: ~$0.005/job, or ~$5/1,000 jobs.
- Apify free $5 monthly credit therefore covers roughly 1,000 richer Indeed rows/month.
- Apify records are richer than Parse compact rows.
- Parse v3 is now cheaper per compact row if paid, and yields more rows on the free tier, but its records remain lighter.

## Evaluation

What worked:

- Free subscribed/public-variant revision path is confirmed.
- A static endpoint can be added without credit cost.
- `search_jobs_rows_compact` can be migrated to the subscribed variant for free.
- Endpoint execution returns compact rows from search page state without per-job detail calls.
- v2/v3 optimization materially improved row yield per runtime call.
- v3 preserved high yield while reducing upstream search calls to one.
- The endpoint is useful for cheap query testing, job-key collection, dedupe, related-query discovery, and first-pass row previews.

What did not change:

- Running endpoints still costs Parse credits.
- Parse compact rows are lighter than Apify exports.
- The endpoint has some relevance drift because it extracts what Indeed search cards expose.
- Apify remains the richer export layer when full job descriptions, apply URLs, benefits, occupation tags, requirements, and company metadata are needed.

New possibilities opened by free revisions:

- Maintain a lightweight subscribed Parse API variant with custom helper endpoints.
- Add cheap post-processing endpoints without paying revision/build cost.
- Add endpoint-specific debug fields before spending runtime credits.
- Create source-specific compact row extractors for other marketplace APIs.
- Prototype small workflow endpoints before deciding whether a tool deserves Incubator/Tool Stack adoption.
- Use static `ping` endpoints as safety checks before larger revisions.
- Optimize runtime yield by revising extraction behavior, limit behavior, filtering, dedupe, and batching.

Guardrails:

- Always verify the target API variant says subscribed/public, not private fork.
- Start with a static no-external-call endpoint to confirm revision routing.
- Do not commit raw API responses, tokens, internal page state, or unredacted output.
- Treat free revisions as iteration savings, not free runtime.
- Use v3 for compact previews; use Apify when richer job data is required.

## Verdict

Tool Stack / Incubator decision:

- Adopt Parse subscribed `search_jobs_rows_compact_v3` as a lightweight compact preview and query-testing layer.
- Keep Apify as the richer bulk export layer for full Indeed job data.
- Keep the ChatGPT Indeed connector as the default interactive review layer.
- Keep Parse platform behavior on a watchlist because the marketplace, versioning, and revision model are evolving quickly.

## Next Step

Stop broad Indeed API testing unless one of these targeted questions becomes useful:

- Can v3 filtering improve relevant-row yield without losing good rows?
- Can `maxPages=2` return 100+ rows for fewer credits than two separate calls?
- Does v3 performance hold on other query types and locations?
- Can a separate Parse Platform Incubator chat track broader marketplace/API evolution?
