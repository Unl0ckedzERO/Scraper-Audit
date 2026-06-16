# The Lab Manifest / Discovery Index

Purpose: make The Lab repo easier for future chats to navigate without requiring exact filenames.

Use this file as the first stop when a chat needs to find relevant workflows, handoffs, decisions, tests, routing rules, naming rules, or sanitized experiment evidence.

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
| Indeed API Incubator | Incubator | Active lane for Indeed API / Parse / Apify scraper testing |
| LLM Council Skill Incubator | Incubator | Active lane for LLM Council / Claude Skill pressure-test experiments |
| Framework | Framework | Main system-design chat for routing, manifests, standards, and repo structure |

Update the active chat map whenever a Lab chat is created, retired, renamed, or materially changes role.

## Discovery Rules for Future Chats

When a user asks about prior Lab work:

1. Search this manifest by plain-language topic first.
2. Search for synonyms, not just exact filenames.
3. Prefer existing test files over memory when evaluating prior evidence.
4. Do not assume a missing manifest entry means no file exists; search the repo if needed.
5. If a useful file is found that is not indexed here, add it to the appropriate section.

Search cues to try:

- Tool names: `Parse`, `Apify`, `Firecrawl`, `Browserbase`, `Indeed`, `GovernmentJobs`
- Workflow types: `scraper`, `job search`, `API`, `row extraction`, `market sizing`, `handoff`, `rubric`, `routing`
- Project zones: `Intake`, `Incubator`, `Framework`, `Archive`
- Outcome terms: `watchlist`, `tool stack`, `dedicated experiment`, `existing project handoff`, `pattern bank`

## Current File Map

### Repository Orientation

| File | Type | Use For | Search Tags |
|---|---|---|---|
| `README.md` | Repo overview | Lab purpose, core zones, routing stages, routing outcomes, logging rules, naming standard | start here, routing, zones, logging, naming |
| `MANIFEST.md` | Discovery index | Finding relevant workflows, tests, handoffs, and framework rules without exact filenames | manifest, index, discovery, handoff, tests |
| `framework/2026-06-15_active_lab_chat_map.md` | Framework / project architecture | Current active Lab chat structure and operating roles | active chats, chat map, Archive, Intake, Incubator, Framework, Indeed API Incubator, LLM Council Skill Incubator |

### Incubator Handoffs

| File | Stage | Summary | Verdict / Route | Search Tags |
|---|---|---|---|---|
| `handoffs/incubator_parse_indeed_search_table_experiment.md` | Incubator Handoff | Handoff for testing whether Parse's Indeed marketplace API can be revised or used differently to return clean job-card rows from search. | Continue as bounded Incubator test; move to Job Search only if Parse can produce clean, affordable rows competitive with Apify. | Parse, Indeed, Incubator, search rows, search_jobs_detailed, Apify comparison, job search handoff |
| `handoffs/intake-to-incubator/2026-06-15-llm-council-claude-skill.md` | Intake → Incubator Handoff | Handoff for testing whether the LLM Council / Claude Skill pressure-test pattern improves Lab routing decisions without overbuilding Intake. | Continue as bounded Incubator proof; move to Framework only if it proves useful as an optional Council Pass rubric. | LLM Council, Claude Skill, pressure-test, Council Pass, sycophancy, validation bias, prompting, Incubator, Framework |

### Indeed / Job Search / Scraper Tests

| File | Stage | Summary | Verdict / Route | Search Tags |
|---|---|---|---|---|
| `tests/2026-05-26_parse_indeed_pipeline_assessment.md` | Evidence Pass / Audit | Parse Indeed API test covering `search_jobs` and `get_job_details`; search returned counts, related queries, pagination/context, and job keys, but not clean job-card rows. Detail endpoint returned usable records by job key. | Keep Parse as selective research probe, not primary sheet extractor. Compare against Apify/connected Indeed before adopting. | Parse, Indeed, search_jobs, get_job_details, job keys, row extraction, market sizing, detail endpoint |
| `tests/2026-05-26_parse_indeed_montana_search_and_revision_hypothesis.md` | Evidence Pass / Audit | Montana `equipment operator` search via Parse; confirmed localized result counts, job keys, pagination, related queries, and missing clean row fields. Defines `search_jobs_detailed` revision hypothesis. | Selective discovery candidate. Do not spend on revision until Apify or another cleaner row-level extractor is tested. | Parse, Indeed, Montana, equipment operator, related queries, pagination, search_jobs_detailed, revision hypothesis |
| `tests/2026-05-26_apify_borderline_indeed_results_evaluation.md` | Evidence Pass / Audit | Apify `borderline/indeed-scraper` returned 20 structured job records with title, company/source, location, job URL, descriptions, dates, job type, and salary for most records. | Strong success. Original cost certainty was pending; see 2026-06-14 Apify paid export evaluation for verified pricing and export-layer routing. | Apify, borderline, Indeed scraper, clean rows, salary, apply URL, dataset, Google Sheets, job search |
| `tests/2026-06-14_apify_indeed_paid_export_layer_evaluation.md` | Incubator / Tool Stack | Apify `borderline/indeed-scraper` follow-up documenting verified `$0.005/job` pricing, 5-row/25-row/100-row runs, rich field coverage, export format guidance, and tool-stack routing. | Adopt as paid bulk export layer after connector/Parse triage; do not use for casual broad sweeps without narrowing. | Apify, Indeed, paid export, $5 per 1000 jobs, row extraction, connector comparison, Parse comparison, Google Sheets, JSON, CSV, Excel |

## Current Decision Index

### Parse vs Apify for Indeed Extraction

Decision: Apify `borderline/indeed-scraper` is currently the stronger implementation candidate for clean row-level Indeed job extraction when a paid export is justified. Parse remains useful as a selective discovery or market-sizing probe when counts, related queries, pagination, and job keys are valuable. The ChatGPT Indeed connector remains the default interactive review tool because it does not add external scraping cost.

Rationale:

- Parse search did not produce clean sheet-ready rows.
- Parse detail calls require job keys and are too expensive for broad extraction if used on every result.
- A Parse fork can normalize rows, but current evidence suggests it bills as search plus per-job detail cost.
- The Indeed connector is strong for interactive search/review, but exposes a limited visible result set at a time.
- Apify produced structured row-level output in one run and follow-up tests verified predictable pricing at `$0.005` per returned job (`$5 / 1,000 jobs`).
- Apify should be used as a paid export layer only after a lane is narrow enough to justify cost.

Use this decision when routing future Indeed scraper work:

- Raw claim or new actor: Intake.
- Controlled actor comparison: Incubator.
- Clean export mapping for an active job-search project: Existing Project Handoff.
- General rules about when a scraper is good enough: Framework.

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
- If mixed:
- If failed:

## Sanitization Notes

Do not commit raw datasets, signed/private links, API keys, credentials, sensitive metadata, or unredacted API responses.
```

## Test Log Standard

Use this structure for new test files in `tests/`:

```md
# [Tool] Test — [Short Outcome-Oriented Name]

Date: YYYY-MM-DD
Zone: Intake / Incubator / Framework / Archive
Tool or Source:
Test Type: API / Scraper / Workflow / Prompt / Business / Data Source / Other
Raw Data Stored: No — only sanitized summary and evaluation are committed.

## Question

What was this test trying to prove or disprove?

## Setup

- Inputs:
- Parameters:
- Baseline or comparison:
- Cost constraints:

## Results

- [Observed result]
- [Observed result]
- [Observed result]

## Field / Output Coverage

| Field / Output | Result | Notes |
|---|---|---|
| Example | Present / Missing / Partial | Short note |

## Evaluation

What worked, what failed, and what is still unknown?

## Verdict

Reject / Archive / Watchlist / Tool Stack / Incubator / Existing Project Handoff / Dedicated Experiment

## Next Step

One clear next action, or `None` if closed.
```

## Naming Standard for New Files

Prefer names that can be understood without opening the file.

### Tests

`tests/YYYY-MM-DD_tool_or_source_short_test_name.md`

Examples:

- `tests/2026-05-26_parse_indeed_pipeline_assessment.md`
- `tests/2026-05-26_apify_borderline_indeed_results_evaluation.md`

### Handoffs

`handoffs/YYYY-MM-DD_source_to_target_short_name.md`

Examples:

- `handoffs/2026-06-14_intake_to_incubator_parse_indeed_search_rows.md`
- `handoffs/2026-06-14_incubator_to_job-search_apify_indeed_export.md`

Existing pre-standard handoff files may remain in place if already referenced, but new handoffs should use the date-prefixed naming pattern.

### Framework Rules

`framework/YYYY-MM-DD_short_rule_or_rubric_name.md`

Examples:

- `framework/2026-06-14_scraper_test_routing_thresholds.md`
- `framework/2026-06-14_tool_stack_adoption_rubric.md`

## Maintenance Template for This Manifest

When adding a new file, append one short row to the most relevant section:

```md
| `path/to/file.md` | Stage or Type | One-sentence summary | Verdict / Route | Search tags |
```

Good search tags include:

- tool name
- source name
- workflow type
- project area
- routing outcome
- key decision words
- common aliases or user phrasing

## Backfill Queue

Use this section for known or suspected prior files that should be indexed later.

| Topic | Likely Area | Why Backfill |
|---|---|---|
| Parse GovernmentJobs / City of Billings test | Tests / Tool Stack | Early Parse proof may be relevant for future government-job scraper or API tests. |
| Scraper Audit naming transition | Framework / Archive | Older notes may still refer to `Scraper-Audit`; index useful files under current `The Lab` naming. |
| Firecrawl / Browserbase / Apify comparison notes | Tests / Framework | Needed for future tool-stack decisions and scraper-routing rules. |
| Intake prompt/rubric rules | Framework | Useful for making first-pass audits consistent without overbuilding weak ideas. |

## Sanitization Reminder

The repo should contain sanitized summaries, decisions, workflows, handoffs, rubrics, and test evaluations.

Do not commit:

- raw datasets
- signed/private links
- API keys
- credentials
- sensitive metadata
- unredacted API responses
- private user records that are not necessary for reusable workflow design

When in doubt, summarize the result and describe the source type instead of preserving raw content.
