# The Lab Manifest / Discovery Index

Purpose: make The Lab repo easier for future chats to navigate without requiring exact filenames.

Use this file as the first stop when a chat needs to find relevant workflows, handoffs, tests, decisions, routing rules, naming rules, or sanitized experiment evidence.

This is a curated index, not a raw data store. Keep entries short, searchable, and sanitized.

## Start Here

1. Read `README.md` for the Lab's zones, routing stages, and logging rules.
2. Read this `MANIFEST.md` to find relevant files by topic, tool, workflow, or routing purpose.
3. Open the linked file(s) before making decisions or running a new test.
4. If a new test or decision is created, append an entry here using the maintenance template below.

## Core Routing Model

The Lab uses this lightweight flow:

1. Inbox
2. Triage
3. Evidence Pass
4. Audit
5. Route

Common route outcomes:

- Reject / Archive
- Pattern Bank
- Watchlist
- Tool Stack
- Incubator
- Existing Project Handoff
- Dedicated Experiment

## Core Zones

| Zone | Use When | Do Not Use For |
|---|---|---|
| Intake | Raw incoming items, first-pass audits, quick tool or idea triage | Heavy implementation, long experiments, mature project work |
| Incubator | Validated ideas, small experiments, tool comparisons, workflow prototypes | Raw unproven ideas, ongoing project implementation |
| Framework | Routing rules, naming rules, architecture, rubrics, thresholds, repo organization | One-off raw idea audits or tool runs unless they define a system rule |
| Archive | Prior mixed work, historical context, old decisions | Active tests unless they are only being referenced historically |

## Active Chat Map

Current active Lab chats are indexed in `framework/2026-06-15_active_lab_chat_map.md`.

Current operating layout:

| Chat | Zone | Role |
|---|---|---|
| Archive | Archive | Historical setup, mixed prior context, and setup validation |
| Intake | Intake | Raw incoming ideas, tools, posts, claims, and first-pass triage |
| LLM Council Skill Incubator | Incubator | Active lane for LLM Council / Claude Skill pressure-test experiments |
| Memory & Organization Layer Evaluation Incubator | Incubator | Active lane for comparing GitHub-only, Airtable, Obsidian, Notion, Cognee, and MemPalace as support layers for project memory, structured tracking, retrieval, and future agent workflows |
| Framework | Framework | Main system-design chat for routing, manifests, standards, and repo structure |

Concluded / handoff-complete Incubator lanes:

| Chat | Former Zone | Outcome |
|---|---|---|
| Instagram Reel Scraper Incubator | Incubator | Testing concluded; current upload path handed off to Intake. Reopen only for workflow fixes, scraper replacement tests, or major evidence-standard revisions. |
| Indeed API Incubator | Incubator | Testing concluded; adopted layered Indeed/Parse/Apify/connector tool stack handed off to Job Search. Reopen only for major Indeed, Parse, Apify, connector, pricing, endpoint, or output-shape changes. |

Update the active chat map whenever a Lab chat is created, retired, renamed, or materially changes role.

## Discovery Rules for Future Chats

When a user asks about prior Lab work:

1. Search this manifest by plain-language topic first.
2. Search for synonyms, not just exact filenames.
3. Prefer existing test files over memory when evaluating prior evidence.
4. Do not assume a missing manifest entry means no file exists; search the repo if needed.
5. If a useful file is found that is not indexed here, add it to the appropriate section.

Search cues to try:

- Tool names: `Parse`, `Apify`, `Firecrawl`, `Browserbase`, `Indeed`, `GovernmentJobs`, `Instagram`, `Airtable`, `Obsidian`, `Notion`, `Cognee`, `MemPalace`
- Workflow types: `scraper`, `job search`, `API`, `row extraction`, `market sizing`, `handoff`, `rubric`, `routing`, `Reel intake`, `evidence bundle`, `tool stack`, `memory layer`, `organization layer`, `structured tracker`, `agent memory`
- Project zones: `Intake`, `Incubator`, `Framework`, `Archive`, `Job Search`
- Outcome terms: `watchlist`, `tool stack`, `dedicated experiment`, `existing project handoff`, `pattern bank`, `closeout`

## Current File Map

### Repository Orientation

| File | Type | Use For | Search Tags |
|---|---|---|---|
| `README.md` | Repo overview | Lab purpose, core zones, routing stages, routing outcomes, logging rules, naming standard | start here, routing, zones, logging, naming |
| `MANIFEST.md` | Discovery index | Finding relevant workflows, tests, handoffs, and framework rules without exact filenames | manifest, index, discovery, handoff, tests |
| `framework/2026-06-15_active_lab_chat_map.md` | Framework / project architecture | Current active and concluded Lab chat structure and operating roles | active chats, concluded chats, chat map, Archive, Intake, Incubator, Framework, LLM Council Skill Incubator, Memory Organization Layer Evaluation Incubator, Instagram Reel Scraper Incubator, Indeed API Incubator |

### Framework Standards / Rules

| File | Stage | Summary | Verdict / Route | Search Tags |
|---|---|---|---|---|
| `framework/2026-06-17_instagram_reel_intake_evidence_standard.md` | Framework / Intake Evidence Standard | Defines evidence tiers and fields Intake should ideally capture for Instagram Reels before routing to Evidence Pass, Incubator, Tool Stack, or project handoff. | Use as the evidence standard behind the adopted Instagram Reel upload workflow; future scraper replacements should compare against this standard. | Instagram, Reel, Reels, short-form video, Intake evidence, screen recording, Apify, scraper, comments, creator metadata, engagement, legitimacy, evidence bundle |

### Incubator Handoffs

| File | Stage | Summary | Verdict / Route | Search Tags |
|---|---|---|---|---|
| `handoffs/2026-06-13_archive_to_incubator_parse_indeed_search_table_experiment.md` | Archive → Incubator Handoff | Original handoff for testing whether Parse's Indeed marketplace API could be revised or used differently to return clean job-card rows from search. | Completed; see closeout test and Incubator → Job Search handoff for adopted tool stack. | Parse, Indeed, Incubator, search rows, search_jobs_detailed, Apify comparison, job search handoff |
| `handoffs/2026-06-15_intake_to_incubator_llm_council_claude_skill.md` | Intake → Incubator Handoff | Handoff for testing whether the LLM Council / Claude Skill pressure-test pattern improves Lab routing decisions without overbuilding Intake. | Continue as bounded Incubator proof; move to Framework only if it proves useful as an optional Council Pass rubric. | LLM Council, Claude Skill, pressure-test, Council Pass, sycophancy, validation bias, prompting, Incubator, Framework |
| `handoffs/2026-06-17_framework_to_incubator_instagram_reel_scraper_intake_evidence_test.md` | Framework → Incubator Handoff | Original handoff for testing Apify Instagram/Reels scrapers and hybrid workflows against the Instagram Reel Intake evidence standard. | Completed; see closeout test and Incubator → Intake handoff for adopted upload path. | Instagram, Reel, Apify, scraper, Intake evidence, screen recording, comments, creator metadata, engagement, legitimacy, Framework, Incubator |
| `handoffs/2026-06-17_incubator_to_intake_instagram_reel_upload_path.md` | Incubator → Intake Handoff | Handoff for the proven Instagram Reel upload path using cheap scrape output, local `whisper.cpp`, and upload-ready ZIP bundles. | Adopt for Intake when a Reel scrape is justified; return to Incubator only for workflow fixes or replacement tests. | Instagram, Reel, Intake, Apify, whisper.cpp, transcript, upload bundle, ZIP, Raw Reels, Refined Reels, scraper workflow |
| `handoffs/2026-06-27_incubator_to_job_search_parse_indeed_api_tool_stack.md` | Incubator → Job Search Handoff | Handoff for the adopted layered Indeed data-source stack: connector for interactive review, Parse rich compact rows, selective Parse details, and Apify rich exports. | Adopt for Job Search; reopen Incubator only for major source, pricing, endpoint, or output-shape changes. | Indeed, Parse, Apify, connector, Job Search, rich_compact_v3, search_jobs_rows, tool stack, handoff, closeout |
| `handoffs/2026-06-29_intake_to_incubator_memory_organization_layer_evaluation.md` | Intake → Incubator Handoff | Handoff for comparing GitHub-only, Airtable, Obsidian, Notion, Cognee, and MemPalace as memory/organization support layers for retrieval, structured tracking, and future agent workflows. | Start as bounded Incubator comparison; GitHub remains the durable ledger unless Framework later changes that. | memory layer, organization layer, Airtable, Obsidian, Notion, Cognee, MemPalace, agent memory, structured tracker, source of truth, Incubator |

### Indeed / Job Search / Scraper Tests

| File | Stage | Summary | Verdict / Route | Search Tags |
|---|---|---|---|---|
| `tests/2026-05-26_parse_indeed_pipeline_assessment.md` | Evidence Pass / Audit | Parse Indeed API test covering `search_jobs` and `get_job_details`; search returned counts, related queries, pagination/context, and job keys, but not clean job-card rows. Detail endpoint returned usable records by job key. | Keep Parse as selective research probe, not primary sheet extractor. Compare against Apify/connected Indeed before adopting. | Parse, Indeed, search_jobs, get_job_details, job keys, row extraction, market sizing, detail endpoint |
| `tests/2026-05-26_parse_indeed_montana_search_and_revision_hypothesis.md` | Evidence Pass / Audit | Montana `equipment operator` search via Parse; confirmed localized result counts, job keys, pagination, related queries, and missing clean row fields. Defines `search_jobs_detailed` revision hypothesis. | Selective discovery candidate; superseded by later Parse row endpoint refinements for table-ready output. | Parse, Indeed, Montana, equipment operator, related queries, pagination, search_jobs_detailed, revision hypothesis |
| `tests/2026-05-26_apify_borderline_indeed_results_evaluation.md` | Evidence Pass / Audit | Apify `borderline/indeed-scraper` returned 20 structured job records with title, company/source, location, job URL, descriptions, dates, job type, and salary for most records. | Strong success. Original cost certainty was pending; see 2026-06-14 Apify paid export evaluation for verified pricing and export-layer routing. | Apify, borderline, Indeed scraper, clean rows, salary, apply URL, dataset, Google Sheets, job search |
| `tests/2026-06-14_apify_indeed_paid_export_layer_evaluation.md` | Incubator / Tool Stack | Apify `borderline/indeed-scraper` follow-up documenting verified `$0.005/job` pricing, 5-row/25-row/100-row runs, rich field coverage, export format guidance, and tool-stack routing. | Adopt as paid bulk export layer after connector/Parse triage; do not use for casual broad sweeps without narrowing. | Apify, Indeed, paid export, $5 per 1000 jobs, row extraction, connector comparison, Parse comparison, Google Sheets, JSON, CSV, Excel |
| `tests/2026-06-27_parse_indeed_api_incubator_closeout.md` | Incubator / Tool Stack | Closeout for the Parse / Indeed API Incubator, documenting the adopted layered Job Search tool stack. | Adopt layered stack for Job Search; close Indeed API Incubator for now. | Parse, Indeed, API, Incubator, closeout, rich_compact_v3, search_jobs_rows, Apify, connector, Job Search tool stack |

### Instagram / Reel Intake / Scraper Tests

| File | Stage | Summary | Verdict / Route | Search Tags |
|---|---|---|---|---|
| `tests/2026-06-17_instagram_reel_scraper_upload_path_closeout.md` | Incubator / Tool Stack | Closeout for the Instagram Reel scraper upload path: cheap scraper media links, local `whisper.cpp` transcription, and ZIP bundles for Intake. | Adopt as Intake upload path when a Reel scrape is justified; keep raw media/JSON out of repo. | Instagram, Reel, Reels, Apify, scraper, whisper.cpp, transcript, Raw Reels, Refined Reels, ZIP bundle, Intake evidence |

### Memory / Organization Layer Tests

| File | Stage | Summary | Verdict / Route | Search Tags |
|---|---|---|---|---|
| `tests/2026-06-29_memory_organization_layer_scorecard_and_sanitized_test.md` | Incubator / Tool Comparison | Lightweight scorecard comparing GitHub-only baseline, Airtable, Obsidian, Notion, Cognee, and MemPalace, plus a narrow sanitized tracker/retrieval probe using repo files only. | Keep GitHub as source of truth; test Airtable-style tracker via repo-native simulation before any external base; defer Cognee/MemPalace to later privacy/security gate. | memory layer, organization layer, structured tracker, Airtable, Obsidian, Notion, Cognee, MemPalace, agent memory, source of truth, sanitized test |

## Current Decision Index

### Parse / Indeed / Apify Job Search Tool Stack

Decision: Indeed job-search extraction should use a layered stack rather than a single source.

Adopted stack:

| Job Search Need | Preferred Source | Notes |
|---|---|---|
| Quick interactive review | ChatGPT Indeed connector | Use first when a small visible set is enough. |
| Compact scoring-ready rows | Parse `search_jobs_rows_rich_compact_v3` style endpoint | Use when row data is needed but full rich export is not justified. |
| Search-state probe / fallback | Parse marketplace search or earlier Parse row endpoints | Use when compact endpoint fails or for market-size/search-term discovery. |
| Selected detail enrichment | Parse detail endpoint | Use only for chosen high-priority jobs. |
| Paid rich export | Apify `borderline/indeed-scraper` | Use for larger/richer datasets when cost is justified. |

Rationale:

- Parse marketplace search did not originally produce clean sheet-ready rows.
- Parse detail calls require job keys and are too expensive for broad extraction if used on every result.
- Parse refined row endpoints created a useful compact-row layer for scoring/review.
- The Indeed connector is strong for interactive search/review, but exposes a limited visible result set at a time.
- Apify produced structured row-level output in one run and follow-up tests verified predictable pricing at `$0.005` per returned job (`$5 / 1,000 jobs`).
- Apify should be used as a paid rich export layer only after a lane is narrow enough to justify cost.

Use this decision when routing future Indeed scraper/API work:

- Normal job-search usage: Job Search project.
- Significant Indeed/Parse/Apify/connector/pricing/output-shape change: reopen Incubator or create a new bounded Incubator test.
- New raw claim or tool: Intake.
- General rules about when a scraper/API is good enough: Framework.

### Instagram Reel Intake Upload Path

Decision: The preferred Intake upload path for selected Instagram Reels is cheap scraper output with transcript/download toggles off, downloaded media from returned links, local `whisper.cpp large-v3-turbo` transcription, and an upload-ready ZIP bundle containing media, transcript, and matching Apify JSON export.

Rationale:

- Tested scraper media links were sufficient to download usable audio/video files.
- Paid Apify transcript and video-download toggles were not necessary by default.
- Local `whisper.cpp` transcription was competitive with the paid transcript toggle and may preserve literal phrasing better in some cases.
- The folder/script workflow produced correctly paired bulk bundles for Intake upload.
- Raw media, signed URLs, and raw JSON should remain local/uploaded to Intake as evidence, not committed to the repo.

Use this decision when routing future Instagram Reel work:

- Raw Reel with no scrape yet: Intake.
- Reel selected for evidence review: use the upload-ready ZIP workflow.
- Scraper/workflow failure or replacement comparison: Incubator.
- Stable operating rule or quick-start: Framework.

## Intake to Incubator Handoff Standard

When moving something from Intake to Incubator, create or include a handoff note with these fields:

```md
# Handoff — [Short Descriptive Name]

Date: YYYY-MM-DD
Source Zone: Intake
Target Zone: Incubator
Item Type: Tool / Workflow / Business Idea / Data Source / Scraper / Other
Status: Proposed Incubator Test

## Why This Passed Intake

- [Initial usefulness proof]
- [What evidence exists]
- [Why it is not just clout/hype]

## What Is Known

- [Confirmed facts]
- [Observed results]
- [Costs or limits, if known]

## What Is Unknown

- [Key unresolved question]
- [Risks or missing proof]

## Incubator Test Question

Can [tool/workflow/idea] do [specific useful outcome] better/cheaper/faster/more reliably than [baseline]?

## Suggested Test

- Input:
- Method:
- Success criteria:
- Stop conditions:
- Expected output:

## Routing After Test

- If successful:
```
