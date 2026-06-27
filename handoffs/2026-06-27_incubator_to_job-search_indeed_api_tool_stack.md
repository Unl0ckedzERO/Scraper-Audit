# Handoff — Indeed API Incubator to Job Search

Date: 2026-06-27
From: Indeed API Incubator
To: Job Search Project
Status: Closeout-ready / adopted tool stack
Raw Data Stored: No — sanitized decision and operating rules only.

## Purpose

This handoff closes the Lab Incubator test for Indeed data-access options and routes the adopted workflow to the Job Search project.

The Lab tested the ChatGPT Indeed connector, Apify `borderline/indeed-scraper`, Parse public/subscribed Indeed endpoints, Parse private-fork behavior, and several custom Parse compact-row endpoints.

## Final Decision

Adopt a layered workflow rather than a single replacement tool.

Current preferred stack:

1. ChatGPT Indeed connector — interactive review and application prep.
2. Parse `search_jobs_rows_rich_compact_v3` — best scoring-ready compact output.
3. Parse `search_jobs_rows_rich_compact_v2` — cheaper normalized rows when scoring metadata is not needed.
4. Parse `search_jobs_rows_compact_v3` — lean fallback and job-key discovery.
5. Parse `get_job_details` — selective enrichment only.
6. Apify Indeed scraper — full rich export and full-description layer.

## What Passed

### Parse rich compact v3

`search_jobs_rows_rich_compact_v3` is the best current Parse endpoint for normalized scoring-ready rows.

Observed reference run:

- Query: `heavy equipment operator`
- Location: `United States`
- Job type: `fulltime`
- Posted window: `14` days
- Limit: `100`
- Max pages: `1`
- Cost: 7 credits
- Rows returned: 59
- Detail calls: 0
- External search calls: 1
- Fallback calls: 0
- Duplicate array values removed: 304
- Opaque/code values dropped: 830

Useful row fields include:

- job key
- title / display title / normalized title
- company
- city / state / postal / formatted location
- salary text and structured salary values
- posted age and timestamp-style dates
- company rating and review count
- employer responsiveness fields
- Indeed Apply flags and resume requirement type
- hiring urgency and hires-needed fields
- remote/sponsored/package fields
- required and preferred requirement labels
- screener requirements
- job type labels
- schedule labels
- benefit labels
- skill/equipment labels
- equipment term matches
- drift flags
- relevance score, bucket, reason, positive signals, and negative signals
- generated Indeed view-job URL

### Parse rich compact v2

`search_jobs_rows_rich_compact_v2` remains useful when normalized rows are needed but relevance scoring is not necessary.

Observed reference run:

- Cost: 6 credits
- Rows returned: 59
- Detail calls: 0
- External search calls: 1

### Parse compact v3

`search_jobs_rows_compact_v3` remains useful as a lean fallback for simple previews and job-key discovery.

Observed reference patterns:

- Around 54–73 rows per call depending on query and location.
- Around 6–8 credits per call.
- No detail calls.
- Best for cheap/simple discovery, not final scoring rows.

### Apify Indeed scraper

Apify remains the best full rich export path.

Use when full descriptions, broad field export, full apply data, or larger structured job-export batches are needed.

Known pricing behavior from tests:

- Approximately $5 per 1,000 jobs.
- 100-result run cost about $0.50.
- $5 monthly credit can cover roughly 1,000 rich jobs if pricing holds.

### ChatGPT Indeed connector

The connector remains useful for free interactive review, application preparation, and manual job-fit analysis.

It is not a bulk export solution because visible results are limited and no clear export-all/pagination/job-key lane was found.

## What Did Not Pass as Primary Layer

### Parse public `search_jobs`

Public `search_jobs` works as discovery/page-state, but it is not sheet-ready.

It exposes raw search-page structures and should not be committed directly. It may include internal or sensitive provider fields that must be sanitized.

### Parse detail enrichment for every row

Do not enrich every row with `get_job_details` by default.

Earlier detail behavior suggested around 2 credits per job. This destroys the cost advantage if used across broad result sets.

Use detail calls only after compact/rich-compact filtering identifies a short list.

### Endpoint-level filtering as default

Endpoint-level include/exclude filters can improve visible row quality, but they reduce returned rows and worsen returned-row cost efficiency.

Prefer broad rich compact extraction first, then filter/rank downstream in the sheet/scoring layer.

## Operating Rules for Job Search

Recommended workflow:

1. Use the Indeed connector for quick interactive searches and fit checks.
2. Use Parse `search_jobs_rows_rich_compact_v3` for scoring-ready preview rows.
3. Load Parse v3 rows into the job-search sheet or scoring model.
4. Filter/rank downstream using relevance score, drift flags, title, salary, location, company, requirements, and user-interest fields.
5. Use `get_job_details` only for a small number of promising rows.
6. Use Apify when a lane needs full descriptions or a larger high-quality export.

Default Parse input shape:

```text
query = <job search query>
location = <city/state, state, or United States>
jt = fulltime
fromage = 14
start = 0
limit = 100
maxPages = 1
dedupe = true
includeExtraDiscovery = false unless testing
```

Use `includeExtraDiscovery = true` only for diagnostic tests or when Parse/Indeed appears to have changed.

## Watch Triggers

Reopen the Incubator lane only if one of these changes:

- Parse updates the public Indeed API output shape.
- Parse adds a better native row/table endpoint.
- Parse changes credit pricing or revision billing.
- Indeed search-card payload changes materially.
- Apify pricing changes materially.
- The ChatGPT Indeed connector gains bulk export, pagination, or job-key access.
- Rich compact endpoints begin failing, returning unsafe fields, or losing key fields.

## Safety Rules

Do not commit:

- raw Indeed/Parse responses
- raw page state
- signed/private links
- tracking URLs
- session/request tokens
- API keys
- cookies
- encoded blobs
- click-handler objects
- ad/ranking/bid fields
- image URLs unless explicitly needed and sanitized
- raw external apply URLs

Commit only sanitized summaries, endpoint behavior, cost observations, and operating rules.

## Closeout Verdict

The Indeed API Incubator test has passed.

Parse is cost-competitive and now quality-competitive for compact scoring previews after the rich compact endpoint revisions. It is not a complete Apify replacement for full-detail exports.

Implementation should move to the Job Search project using the layered stack above.
