# Project Migration Recommendation

Date created: 2026-05-30  
Updated: 2026-06-13  
Context: Current mixed audit chat covering Reels/business opportunity intake, tool testing, scraper/API evaluation, and framework design.

## Recommendation

Yes: keep the current mixed chat inside `The Lab`, but treat it as the historical archive rather than the clean future intake chat.

Create new chats inside the project for specific functions.

## Project Name

Use:

`The Lab`

## What This Project Should Contain

The project should contain:

- this existing mixed chat as `Archive — Audit Lab v0 / Mixed Chat`
- a clean intake chat for new Reels/posts/tools
- an incubator chat for ideas/tools that passed initial audits but do not yet belong elsewhere
- a framework chat for architecture and system-design questions
- `Unl0ckedzERO/The-Lab` as the external Git ledger/reference

## Recommended Chats Inside the Project

### 1. `Intake — Reels, Tools, Ideas`

Purpose:

- receive new posts, videos, screenshots, transcripts, links, tool claims, creator claims, shopping/lifestyle/education ideas, and workflow ideas
- perform first-pass audits only
- avoid long implementation branches

### 2. `Incubator — Validated Ideas + Tool Tests`

Purpose:

- mature ideas that passed initial usefulness proof but do not yet belong to a separate existing project
- run small tests
- compare tools
- develop temporary workflows
- prepare handoffs once a project home becomes clear

### 3. `Framework — Audit System Design`

Purpose:

- discuss routing rules, project structure, intake categories, scoring rubrics, thresholds, naming schemes, and process design
- keep meta-questions out of the intake chat

### 4. `Archive — Audit Lab v0 / Mixed Chat`

Purpose:

- preserve historical context
- reference prior decisions and tests
- do not use as the primary clean intake going forward

## What Should Not Live Permanently Here

Do not use this project as the final home for mature implementation work when a clearer project exists.

Examples:

- Apify-to-Sheets Indeed implementation -> Job Search project
- trading strategy implementation -> Trading project
- resume workflows -> relevant resume project
- AI course/course mirror work -> AI course project

## Why This Works

Moving the current chat into The Lab preserves useful context without forcing future intake to stay mixed.

New chats inside the project allow clean separation between:

- raw intake
- incubation/testing
- framework design
- project handoffs

GitHub remains useful for durable, sanitized workflows and logs, but it does not replace conversational separation.

## Project Instruction Draft

This project is an audit lab for evaluating incoming ideas, tools, Reels/posts, workflow opportunities, and data-source/scraper experiments. Keep early intake lightweight and avoid over-building weak ideas. Use routing stages: Inbox, Triage, Evidence Pass, Audit, Route. When an idea passes initial usefulness proof and belongs to an existing project, create a handoff and move implementation there. When an idea is promising but has no project home, move it from Intake to Incubator. Use the GitHub repo `Unl0ckedzERO/The-Lab` as the durable ledger for sanitized workflows, tool tests, decisions, routing rules, naming rules, and project handoff notes. Do not commit raw datasets, signed/private links, API keys, or sensitive metadata; summarize and sanitize before logging. Avoid HVAC/work-realism bias unless explicitly requested. Treat clout as a signal, not validation.

## Decision Rule

Keep this mixed chat as archive/context. Create new chats inside The Lab if the goal is to keep future intake clean.
