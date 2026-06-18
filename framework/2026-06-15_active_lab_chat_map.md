# Active Lab Chat Map

Date: 2026-06-17
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
| Indeed API Incubator | Incubator | Active incubator lane for Indeed API / Parse / Apify scraper testing | Handles bounded tests around job-search scraping, paid export layers, row extraction, and connector/API comparisons. |
| LLM Council Skill Incubator | Incubator | Active incubator lane for the LLM Council / Claude Skill pressure-test idea | Handles bounded tests of whether a council-style critique pass improves Lab routing decisions without overbuilding Intake. |
| Framework | Framework | Main system-design chat for The Lab | Owns routing rules, naming rules, manifests, handoff standards, rubrics, thresholds, and repo structure. |

## Concluded / Handoff-Complete Incubator Chats

| Chat | Former Zone | Outcome | Notes |
|---|---|---|---|
| Instagram Reel Scraper Incubator | Incubator | Concluded testing; handed off to Intake | Produced the current preferred Instagram Reel upload path using cheap Apify scrape output, local `whisper.cpp`, and upload-ready ZIP bundles. Return here only for workflow fixes or replacement tests. |

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

The Lab currently has two active Incubator chats:

1. Indeed API Incubator
2. LLM Council Skill Incubator

Instagram Reel Scraper Incubator is no longer an active test lane; its result is now an Intake upload workflow. Reopen or create a new bounded Incubator test only if the workflow fails, a scraper replacement is being compared, or the evidence standard needs a major revision.

## When to Update This File

Update this file when:

- a new Lab chat is created
- a chat is retired or moved to Archive
- an Incubator lane graduates into an existing project handoff
- a new durable operating zone is created
- the role of a current chat materially changes
