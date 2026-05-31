# Project Migration Recommendation

Date created: 2026-05-30  
Context: Current mixed audit chat covering Reels/business opportunity intake, tool testing, scraper/API evaluation, and framework design.

## Recommendation

Yes: move the current chat into a dedicated project, but treat it as the historical lab/archive rather than the clean future intake chat.

Create new chats inside that project for specific functions.

## Suggested Project Name

Recommended:

`Opportunity + Tool Audit Lab`

Other acceptable names:

- `Audit Lab`
- `Opportunity Intake + Tool Testing`
- `Scraper + Opportunity Audit`

## What This Project Should Contain

The project should contain:

- this existing mixed chat as `Audit Lab v0 / Archive`
- new clean intake chat for new Reels/posts/tools
- separate lab/incubator chat for ideas that passed initial audits
- optional system/framework chat for architecture questions
- Scraper Audit repo as the external ledger/reference

## Recommended Chats Inside the Project

### 1. `Intake — Reels, Tools, Ideas`

Purpose:

- receive new posts, videos, screenshots, transcripts, links, tool claims, creator claims, shopping/lifestyle/education ideas, and workflow ideas
- perform first-pass audits only
- avoid long implementation branches

### 2. `Lab — Validated Ideas + Tool Tests`

Purpose:

- mature ideas that passed initial usefulness proof but do not yet belong to a separate existing project
- run small tests
- compare tools
- develop temporary workflows

### 3. `Framework — Audit System Design`

Purpose:

- discuss routing rules, project structure, intake categories, scoring rubrics, thresholds, and process design
- keep meta-questions out of the intake chat

### 4. Current Chat: `Audit Lab v0 / Mixed Archive`

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

Moving the current chat into a project preserves useful context without forcing future intake to stay mixed.

New chats inside the project allow clean separation between:

- raw intake
- incubation/testing
- framework design
- project handoffs

GitHub remains useful for durable, sanitized workflows and logs, but it does not replace conversational separation.

## Project Instruction Draft

This project is an audit lab for evaluating incoming ideas, tools, Reels/posts, workflow opportunities, and data-source/scraper experiments. Keep early intake lightweight and avoid over-building weak ideas. Use routing stages: Inbox, Triage, Evidence Pass, Audit, Route. When an idea passes initial usefulness proof and belongs to an existing project, create a handoff and move implementation there. When an idea is promising but has no project home, move it from Intake to Lab/Incubator. Keep raw datasets and signed/private links out of GitHub; log sanitized summaries, workflows, costs, and decisions instead. Avoid HVAC/work-realism bias unless explicitly requested. Treat clout as a signal, not validation.

## Decision Rule

Move this chat into a project if the goal is to preserve and reuse the architecture and tool-test context.

Create new chats inside the project if the goal is to keep future intake clean.

Do both.
