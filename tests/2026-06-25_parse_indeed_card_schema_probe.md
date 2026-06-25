# Parse Indeed Test — Search Card Schema Probe

Date: 2026-06-25
Zone: Incubator
Tool or Source: Parse `indeed.com` subscribed API variant
Test Type: Schema discovery / API quality improvement
Raw Data Stored: No — sanitized summary only.

## Question

Can Parse improve beyond snippet-level compact rows by extracting additional safe fields already present in the Indeed search-card payload, without calling job detail pages?

## Setup

Endpoint tested: `search_jobs_card_schema_probe`

Key inputs:

- query: `heavy equipment operator`
- location: `United States`
- `jt`: `fulltime`
- `fromage`: `14`
- `start`: `0`
- `maxPages`: `1`
- `sampleSize`: `10`

## Results

Sanitized summary:

- Cost: 6 credits.
- `totalJobCount`: about 2,200.
- `cardsFound`: 43.
- `cardsSampled`: 10.
- `detailCallsMade`: 0.
- `externalSearchCallsMade`: 1.
- `fallbackSearchCallsMade`: 0.
- Search-card schema contained materially more fields than the earlier compact row extractor used.

Useful safe candidates found in the card payload include:

- Structured salary fields: salary text, min, max, currency, type/source.
- Posting date fields: relative age plus timestamp-style publish/create dates.
- Company quality fields: company rating and review count.
- Apply-path fields: Indeed Apply flags and resume requirement type.
- Hiring urgency fields: urgent hiring, hiring event, high-volume hiring, hires-needed fields.
- Employer response fields: employer responsive and response-time fields.
- Location fields: formatted location, city, state, postal code, location count, extra-location label.
- Remote flag.
- Sponsored/paid placement flags.
- Job requirements/tags: requirement labels, strictness, screener labels, screener question type.
- Job type/taxonomy labels.
- Benefit/tag arrays from ranked-benefits/taxonomy areas.

Important safety issue:

The probe also surfaced many fields that should not be carried into a durable row extractor, even when the probe marked some of them as safe or useful. Avoid raw tracking, token/session-like, encoded, ranking, ad, internal, and image URL fields.

Examples of categories to exclude from future extraction:

- Tracking URLs and tracking fields.
- Session or request token fields.
- Encoded blobs and encrypted/internal IDs.
- Ad/bid/ranking/scoring fields.
- Mouse/click handler objects.
- Branding image URLs.
- Campaign IDs and internal feed/homepage section IDs.
- Screener URLs or application URLs unless explicitly sanitized and needed.

## Evaluation

The schema probe confirms Parse quality can be improved without detail calls. A richer compact endpoint can likely add structured salary, company rating/review count, posting dates, apply flags, urgency/hiring flags, location normalization, requirements, taxonomy/job type labels, benefits/tags, and remote/sponsored indicators.

This would not equal Apify's full-detail export because full descriptions and rich apply metadata still require detail or richer scrape layers. However, it would make Parse much more useful as a compact preview/scoring layer.

The schema probe's automated recommendation list is too broad and too trusting. Future extraction should use a strict manual whitelist.

## Verdict

Proceed with a `search_jobs_rows_rich_compact_v1` endpoint only if it uses a strict whitelist and excludes internal/unsafe fields.

Do not copy all recommended fields from the schema probe.

## Recommended Whitelist for Rich Compact v1

Core fields:

- `jobkey`
- title / display title / normalized title
- company
- formatted location
- city / state / postal if available
- salary text
- salary min / max / type / currency if available
- posted age
- publish/create date if available
- job URL built from job key
- source

Quality/scoring fields:

- company rating
- company review count
- remote flag
- sponsored flag
- urgently hiring flag
- high-volume hiring flag
- hiring event flag
- hires needed / hires needed exact
- employer responsive flag
- employer response time
- Indeed Apply enabled/applyable flags
- resume type if available
- location count / additional-location label

Text arrays:

- requirement labels with strictness
- screener requirement labels and types
- job type labels
- taxonomy labels
- benefits/tags labels

Guardrails:

- No raw card objects.
- No raw provider state.
- No tracking URLs.
- No token/session-like fields.
- No encoded blobs.
- No image URLs.
- No ad/bid/ranking scores.
- No click/mouse handler objects.
- No raw external apply URLs unless sanitized and explicitly required.
