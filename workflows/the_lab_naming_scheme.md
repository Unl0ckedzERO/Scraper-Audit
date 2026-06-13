# The Lab Naming Scheme

Date created: 2026-06-13  
Updated: 2026-06-13  
Scope: Chat/project/repo naming conventions for The Lab project.

## Core Decision

Use `The Lab` as the umbrella project name.

Use `Incubator` for validated ideas and tool tests that passed initial intake but do not yet belong to an existing project.

This avoids confusion between the project name (`The Lab`) and the maturation space (`Incubator`).

## Final Recommended Chat Names

### `Intake — Reels, Tools, Ideas`

Purpose:

- New incoming Reels/posts/videos/tools/ideas.
- First-pass audits.
- Light triage only.
- Avoid long implementation branches.

Opening context phrase:

`This chat will be used for Intake as defined in The Lab / Git repo.`

### `Incubator — Validated Ideas + Tool Tests`

Purpose:

- Ideas or tools that passed initial usefulness proof.
- No clear existing project home yet.
- Small experiments, tool comparisons, and hypothesis refinement.
- Later handoff to an existing project or dedicated project if it matures.

Opening context phrase:

`This chat will be used for Incubator work as defined in The Lab / Git repo.`

### `Framework — Audit System Design`

Purpose:

- System design for The Lab itself.
- Routing rules, thresholds, naming schemes, project architecture, rubrics, and process revisions.
- Keeps meta-architecture out of Intake.

Opening context phrase:

`This chat will be used for Framework work as defined in The Lab / Git repo.`

### `Archive — Audit Lab v0 / Mixed Chat`

Purpose:

- Historical mixed chat/archive.
- Contains the original development of the Reels/business audit, Parse/Firecrawl/Apify testing, job-search handoff work, and framework decisions.
- Useful for reference, but not the clean future Intake space.

## Current Repo Reference

Use:

`Unl0ckedzERO/The-Lab`

This repository was originally named `Scraper-Audit`. Older notes, commits, and references may use that name. Going forward, use `The Lab` for the project and `Unl0ckedzERO/The-Lab` for the repository.

## Suggested Umbrella Terms

- `The Lab`: the overall project / operating system
- `Intake`: raw incoming material
- `Triage`: initial classification and usefulness check
- `Evidence Pass`: lightweight evidence gathering
- `Audit`: structured evaluation
- `Route`: archive, pattern bank, incubator, project handoff, or reject
- `Incubator`: validated but not yet project-homed ideas/tools
- `Framework`: system and process design
- `Archive`: historical mixed context

## Recommended Project Instruction Line

`Use the GitHub repo Unl0ckedzERO/The-Lab as the durable ledger for sanitized workflows, tool tests, decisions, routing rules, naming rules, and project handoff notes.`

## Assessment

The naming system is clear in intent.

It separates:

- the overall project (`The Lab`)
- raw intake (`Intake`)
- mature-but-unhomed ideas (`Incubator`)
- meta/system work (`Framework`)
- historical context (`Archive`)

This should reduce chat clutter while still allowing future random Reels/tools/ideas to influence maturing concepts through routed handoff notes rather than direct blending.
