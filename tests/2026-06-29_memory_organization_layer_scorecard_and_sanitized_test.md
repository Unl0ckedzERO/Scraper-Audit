# Memory & Organization Layer Evaluation — Lightweight Scorecard + Narrow Sanitized Test

Date: 2026-06-29
Zone: Incubator
Status: Active bounded comparison
Source handoff: `handoffs/2026-06-29_intake_to_incubator_memory_organization_layer_evaluation.md`

## Purpose

Compare GitHub-only baseline, Airtable, Obsidian, Notion, Cognee, and MemPalace as possible support layers for The Lab project memory, structured tracking, retrieval, and future agent workflows.

This is not an adoption decision. It is a lightweight Incubator scorecard plus one narrow sanitized test design.

## Baseline Rule

GitHub remains the durable source of truth for The Lab unless a later Framework decision explicitly changes that.

Support layers may hold indexes, trackers, dashboards, or working notes, but durable decisions, test outcomes, standards, routing rules, and handoffs should continue to be summarized and sanitized into this repo.

## Hard Exclusions

Do not ingest or commit:

- raw datasets
- signed/private links
- API keys
- credentials
- raw Reel ZIPs
- private exports
- raw Apify/Parse JSON exports
- unredacted tool traces
- sensitive metadata
- unrelated private account data

## Current Best-Fit Roles

| Layer | Candidate | Initial Role | Adoption Posture |
|---|---|---|---|
| Durable ledger | GitHub-only baseline | Source of truth for sanitized decisions, handoffs, tests, standards, and manifest/index discovery | Keep |
| Structured tracker | Airtable | Optional tracker for Watchlist, Intake, Incubator candidates, Reel records, scraper tests, rankings, statuses, and next actions | Test first via repo-native table/CSV simulation |
| Personal thinking layer | Obsidian | Local Markdown thinking map and cross-project idea graph | Optional user-side practice; not a Lab source of truth |
| Human-facing dashboard | Notion | Polished dashboard/wiki for human review | Use sparingly; high duplication risk |
| Agent memory / graph retrieval | Cognee | Semantic + graph memory over sanitized trusted docs; possible future MCP/agent memory infrastructure | Test later behind privacy/security gate |
| Local-first verbatim agent memory | MemPalace | Possible local-first verbatim retrieval layer for sanitized project/session memory | Watch/test later; verify claims before adoption |

## Scorecard Method

Score scale: 1–5. Higher is better.

For friction, maintenance, and source-of-truth risk, higher means lower friction, lower maintenance burden, and lower risk.

| Candidate | Retrieval quality | Structured data | Human readability | Agent compatibility | Privacy / control | Setup friction | Maintenance burden | Export / backup | Low source-of-truth risk | Fit for The Lab | Fit for other projects | Total / 55 | Initial Route |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---|
| GitHub-only baseline | 3 | 2 | 4 | 4 | 5 | 5 | 4 | 5 | 5 | 5 | 4 | 46 | Keep baseline |
| Airtable | 3 | 5 | 4 | 4 | 3 | 4 | 3 | 3 | 3 | 4 | 5 | 41 | Test tracker layer |
| Obsidian | 4 | 3 | 4 | 3 | 5 | 3 | 3 | 5 | 3 | 3 | 4 | 40 | Optional user-side layer |
| Notion | 4 | 4 | 5 | 4 | 3 | 4 | 2 | 3 | 2 | 3 | 4 | 38 | Watch / use sparingly |
| MemPalace | 4 | 2 | 2 | 4 | 4 | 3 | 3 | 3 | 3 | 3 | 3 | 34 | Watch; test later |
| Cognee | 4 | 3 | 2 | 5 | 3 | 2 | 2 | 3 | 3 | 3 | 3 | 33 | Test later behind gate |

## Initial Read

1. GitHub-only is still the strongest baseline because it is durable, searchable, versioned, exportable, and already working.
2. Airtable has the best immediate upside because The Lab already has many structured objects: Reels, Watchlist items, Incubator candidates, tool tests, scores, statuses, routes, and next actions.
3. Obsidian could help personal thinking, but it should not become an official Lab decision store unless a later Framework decision changes the operating model.
4. Notion is useful for dashboards and human-facing pages, but it has the highest risk of becoming polished duplication.
5. Cognee and MemPalace are interesting for future agent workflows, but both should be tested only on sanitized repo files and only after a privacy/security gate.

## Narrow Sanitized Test — Phase 1

### Test Name

`memory_layer_minimum_tracker_probe`

### Test Question

Can an Airtable-style structured tracker improve Lab continuity and sorting/filtering compared with GitHub-only notes, without creating a second source of truth?

### Inputs

Use only sanitized repo files and manually created records from those files:

- `README.md`
- `MANIFEST.md`
- `framework/2026-06-15_active_lab_chat_map.md`
- `handoffs/2026-06-29_intake_to_incubator_memory_organization_layer_evaluation.md`
- `framework/2026-06-17_instagram_reel_intake_evidence_standard.md`
- `handoffs/2026-06-17_incubator_to_intake_instagram_reel_upload_path.md`
- `tests/2026-06-17_instagram_reel_scraper_upload_path_closeout.md`
- `handoffs/2026-06-27_incubator_to_job_search_parse_indeed_api_tool_stack.md`
- `tests/2026-06-27_parse_indeed_api_incubator_closeout.md`

### Method

Do not start with Airtable itself. First simulate the tracker inside the repo as a Markdown table or CSV-style schema.

Create 8–12 manually written sanitized records with no raw evidence attached. Each record should point back to repo files rather than duplicate the underlying decision.

### Proposed Tracker Fields

| Field | Type | Purpose |
|---|---|---|
| Record ID | Short text | Stable tracker key, e.g. `LAB-MEM-001` |
| Item | Text | Short human-readable name |
| Zone | Single select | Intake, Incubator, Framework, Archive, Existing Project |
| Stage | Single select | Inbox, Triage, Evidence Pass, Audit, Route, Closeout |
| Route | Single select | Watchlist, Tool Stack, Incubator, Existing Project Handoff, Pattern Bank, Reject / Archive |
| Candidate Tool | Multi-select | GitHub, Airtable, Obsidian, Notion, Cognee, MemPalace, Parse, Apify, etc. |
| Project Fit | Multi-select | The Lab, Intake, Job Search, AIA, Reel Intake, Tool Stack, etc. |
| Current Verdict | Single select | Keep, Test, Watch, Reject, Adopted, Closed |
| Confidence | 1–5 number | How proven the item is |
| Maintenance Cost | 1–5 number | Higher means easier to maintain |
| Source-of-Truth Risk | 1–5 number | Higher means lower risk |
| Next Action | Text | One concrete next action |
| Source File | Text/path | Repo path to authoritative source |
| Last Reviewed | Date | Review hygiene |
| Notes | Text | Short sanitized note only |

### Sample Sanitized Records

| Record ID | Item | Zone | Stage | Route | Candidate Tool | Current Verdict | Next Action | Source File |
|---|---|---|---|---|---|---|---|---|
| LAB-MEM-001 | Memory & Organization Layer Evaluation | Incubator | Audit | Incubator | GitHub, Airtable, Obsidian, Notion, Cognee, MemPalace | Test | Run tracker probe; do not install agent memory yet | `handoffs/2026-06-29_intake_to_incubator_memory_organization_layer_evaluation.md` |
| LAB-MEM-002 | Lab durable ledger rule | Framework | Route | Tool Stack | GitHub | Keep | Preserve GitHub as source of truth | `README.md` |
| LAB-MEM-003 | Manifest discovery rule | Framework | Route | Tool Stack | GitHub | Keep | Keep new tests indexed in MANIFEST | `MANIFEST.md` |
| LAB-MEM-004 | Instagram Reel upload path | Intake | Closeout | Tool Stack | Apify, whisper.cpp, GitHub | Adopted | Use ZIP bundle workflow for selected Reels | `tests/2026-06-17_instagram_reel_scraper_upload_path_closeout.md` |
| LAB-MEM-005 | Indeed / Parse / Apify tool stack | Existing Project | Closeout | Existing Project Handoff | Parse, Apify, Indeed connector | Adopted | Use layered job-search stack in Job Search project | `tests/2026-06-27_parse_indeed_api_incubator_closeout.md` |
| LAB-MEM-006 | Airtable-style tracker | Incubator | Evidence Pass | Watchlist | Airtable | Test | Simulate fields in repo before creating external base | this file |
| LAB-MEM-007 | Cognee retrieval layer | Incubator | Triage | Watchlist | Cognee | Watch | Test only on sanitized repo docs after privacy/security gate | this file |
| LAB-MEM-008 | MemPalace retrieval layer | Incubator | Triage | Watchlist | MemPalace | Watch | Verify official setup and run only sanitized retrieval test | this file |

## Test Questions

Run these against the GitHub-only baseline and the simulated tracker.

1. What did we decide about Instagram Reel upload bundles?
2. What belongs in Watchlist vs Incubator?
3. Which handoff naming/source-of-truth rule are we using?
4. What should never be committed to the repo?
5. Which Parse/Indeed tests have already happened?
6. Which tools are currently under memory/organization evaluation?
7. Which items need next action?
8. Which active Incubator lanes exist?

## Measurement Rubric

| Dimension | Pass Signal | Fail Signal |
|---|---|---|
| Retrieval accuracy | Correct answer points to the right source file | Missed file, stale answer, or vague memory-only answer |
| Source grounding | Answer can name the repo file that supports it | Answer cannot trace back to an authoritative repo source |
| Structured usefulness | Tracker can sort/filter by tool, route, stage, next action, and project fit | Tracker adds no value beyond MANIFEST search |
| Maintenance cost | Fields are simple enough to update during normal closeout | Requires heavy duplicate upkeep |
| Privacy | No raw/private evidence needed | Needs raw datasets, signed links, exports, or private metadata |
| Source-of-truth safety | Tracker points to repo decisions instead of replacing them | Tracker becomes a competing decision store |

## Pass / Fail Threshold

Airtable or Airtable-style tracking earns a real Airtable test only if the simulated tracker clearly improves at least two of these:

- sorting/filtering Watchlist and Incubator candidates
- seeing next actions across tools
- comparing candidates by route/status/confidence
- reducing repeated setup/context explanation
- helping agents select the right source files before answering

It should be downgraded if it mostly duplicates `MANIFEST.md`.

## Minimum Viable Stack Recommendation

### Now

- GitHub repo as source of truth.
- `README.md` for high-level operating model.
- `MANIFEST.md` for discovery.
- Test files and handoffs for durable decisions.
- One repo-native tracker simulation before any external base is created.

### Next Only If Useful

- Airtable for structured status/ranking/next-action tracking if the simulated tracker proves useful.
- Obsidian only as a personal thinking map, not as Lab authority.
- Notion only for dashboard/readout pages if a human-facing view becomes useful.

### Later Gate

- Cognee and MemPalace only after a second bounded test focused on privacy, local storage behavior, retrieval source-grounding, exportability, and MCP/agent permissions.

## Current Route

| Candidate | Current Route | Why |
|---|---|---|
| GitHub-only baseline | Keep | Working durable ledger and discovery base |
| Airtable | Test | Strongest immediate fit for structured tracker layer |
| Obsidian | Watch / optional | Useful for thinking, weak as official tracker |
| Notion | Watch / use sparingly | Strong dashboard UX, high duplication risk |
| Cognee | Test later | Strong agent-memory direction, heavier setup/security review needed |
| MemPalace | Watch / test later | Interesting local/verbatim memory direction, claims need verification |

## External Verification Notes

Checked on 2026-06-29 at a lightweight level only:

- Airtable currently presents itself as an app-building / relational-data platform with interfaces, automations, integrations, and AI/agent features.
- Obsidian supports structured note properties stored as YAML and remains a strong local Markdown-style thinking layer.
- Notion supports databases/API access and exports pages/databases as HTML, Markdown, and CSV, but export/re-import is not a perfect source-of-truth replacement.
- Cognee documentation describes an AI memory platform with relational, vector, and graph stores plus MCP integration and self-hosted security controls.
- MemPalace needs more verification from official project materials before any real adoption decision; treat current claims as Watchlist evidence only.

## Next Action

Use this file as the first test artifact. The next Incubator step should be to answer the eight test questions using:

1. GitHub-only retrieval via `README.md`, `MANIFEST.md`, handoffs, and closeout files.
2. This simulated tracker table.

Then decide whether Airtable deserves an actual external-base test, or whether the repo-native tracker plus `MANIFEST.md` is enough.
