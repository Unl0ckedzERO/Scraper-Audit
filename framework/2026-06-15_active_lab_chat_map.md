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
| Instagram Reel Scraper Incubator | Incubator | Active incubator lane for Instagram Reel scraper / Intake evidence workflow testing | Handles bounded comparisons of Apify Instagram/Reels scrapers and hybrid evidence workflows against the Framework Reel Intake evidence standard. |
| Framework | Framework | Main system-design chat for The Lab | Owns routing rules, naming rules, manifests, handoff standards, rubrics, thresholds, and repo structure. |

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

The Lab currently has three active Incubator chats:

1. Indeed API Incubator
2. LLM Council Skill Incubator
3. Instagram Reel Scraper Incubator

New Incubator chats should only be created when a validated idea needs its own bounded experiment lane and would clutter the general Incubator pattern.

## When to Update This File

Update this file when:

- a new Lab chat is created
- a chat is retired or moved to Archive
- an Incubator lane graduates into an existing project handoff
- a new durable operating zone is created
- the role of a current chat materially changes
