# Active Lab Chat Map

Date: 2026-06-27
Type: Framework / Project Architecture
Status: Current operating map

## Purpose

This file records the active ChatGPT chat structure for The Lab so future chats can understand how work is divided without relying on memory or exact prior conversation access.

The chat map is structural context only. Raw tests, datasets, private links, and sensitive metadata should not be copied here.

## Active Chats

| Chat | Zone | Current Role | Notes |
|---|---|---|---|
| Archive | Archive | Historical setup, mixed prior context, setup validation | Used to check that the Lab structure, repo, and routing basics are set up properly. |
| Intake | Intake | Raw incoming ideas, tools, posts, claims, and first-pass triage | Should stay lightweight; mature or useful ideas should not remain here indefinitely. |
| LLM Council Skill Incubator | Incubator | Active incubator lane for the LLM Council / Claude Skill pressure-test idea | Handles bounded tests of whether a council-style critique pass improves Lab routing decisions without overbuilding Intake. |
| Framework | Framework | Main system-design chat for The Lab | Owns routing rules, naming rules, manifests, handoff standards, rubrics, thresholds, and repo structure. |

## Concluded / Handoff-Complete Incubator Chats

| Chat | Former Zone | Outcome | Notes |
|---|---|---|---|
| Instagram Reel Scraper Incubator | Incubator | Concluded testing; handed off to Intake | Produced the current preferred Instagram Reel upload path using cheap Apify scrape output, local `whisper.cpp`, and upload-ready ZIP bundles. Return here only for workflow fixes or replacement tests. |
| Indeed API Incubator | Incubator | Concluded testing; handed off to Job Search | Produced the adopted Indeed API tool stack: Parse `search_jobs_rows_rich_compact_v3` for scoring-ready compact rows, Parse v2/v3 fallbacks, selective Parse detail calls, Apify for full rich exports, and the Indeed connector for interactive review. Reopen only for significant Indeed/Parse/API/pricing changes or endpoint failure. |

## Operating Rule

Framework should understand the other chats as operating zones, but should not duplicate their work.

Use Framework for:

- deciding where a chat or workflow belongs
- creating durable routing rules
- updating repo indexes and manifests
- creating handoff standards
- diagnosing structure issues across chats
- turning repeated behavior into reusable Lab rules

Do not use Framework for:

- raw first-pass audits that belong in Intake
- long bounded tool experiments that belong in Incubator
- implementation inside an existing non-Lab project
- storing raw datasets or sensitive evidence

## Current Incubator Chats

The Lab currently has one active Incubator chat:

1. LLM Council Skill Incubator

Instagram Reel Scraper Incubator is no longer an active test lane; its result is now an Intake upload workflow. Reopen or create a new bounded Incubator test only if the workflow fails, a scraper replacement is being compared, or the evidence standard needs a major revision.

Indeed API Incubator is no longer an active test lane; its result is now a Job Search tool stack. Reopen or continue that chat only if Indeed, Parse, Apify, or the connector changes materially, or if the adopted endpoints fail.

## When to Update This File

Update this file when:

- a new Lab chat is created
- a chat is retired or moved to Archive
- an Incubator lane graduates into an existing project handoff
- a new durable operating zone is created
- the role of a current chat materially changes
