# Handoff — Instagram Reel Scraper / Intake Evidence Test

Date: 2026-06-17
Source Zone: Framework
Target Zone: Incubator
Item Type: Tool / Workflow / Scraper / Intake Evidence
Status: Proposed Incubator Test

## Purpose

Test which collection strategy best improves Instagram Reel Intake evidence without making Intake heavy or expensive.

This handoff exists because Framework has defined the target evidence standard, but the actual scraper/tool comparison should happen in a bounded Incubator lane.

## Source Standard

Use this Framework file as the target evidence specification:

`framework/2026-06-17_instagram_reel_intake_evidence_standard.md`

The Incubator test should evaluate candidate scrapers/workflows against that standard, not invent a new evidence model from scratch.

## Why This Passed Framework

- The current screen-recording workflow is free and low-friction, but it can lose important evidence such as caption text, creator metadata, engagement counts, post age, comments, links, and legitimacy signals.
- The user already selects specific Reels before testing, so the target workflow only needs to scrape known Reel URLs, not discover thousands of Reels.
- The expected volume is low enough that a cheap paid-per-Reel enrichment workflow may be worthwhile.
- The outcome could improve all future Intake decisions and Intake-to-Incubator handoffs.

## What Is Known

- Current baseline: user sends screen recordings of Instagram Reels to Intake, sometimes with extra links.
- Screen recordings remain useful as Tier 0 context because they preserve visual/audio context cheaply.
- Apify has multiple Instagram-style scrapers available.
- User has done early Apify Instagram scraper tests and observed that known-Reel scraping appears relatively cheap.
- Framework has defined evidence tiers:
  - Tier 0: lightweight screen recording
  - Tier 1: standard Reel evidence bundle
  - Tier 2: enriched legitimacy bundle
  - Tier 3: deep audit inputs
- The likely final workflow is hybrid: screen recording for low-friction context plus scrape bundle when the Reel is promising.

## What Is Unknown

- Which Apify Instagram scraper best supports known Reel URLs.
- Which scraper returns the cleanest caption, creator metadata, engagement fields, comments, post date, and links.
- Whether any scraper reliably returns enough comment data to judge audience quality.
- Whether transcript/on-screen-text capture is available from scraper output or needs a separate step.
- True cost per useful Reel after retries, failed runs, and cleanup.
- Whether the output can be sanitized easily before any repo logging.
- Whether a scraper can replace screen recordings entirely or should only supplement them.

## Incubator Test Question

Can an Apify Instagram/Reels scraper or hybrid collection workflow produce a Tier 1 or Tier 2 Intake evidence bundle for selected Instagram Reels more reliably and usefully than screen recording alone, at an acceptable cost per Reel?

## Candidate Strategies to Compare

1. Screen recording only baseline
2. Screen recording + manual link/caption notes
3. Apify known-Reel scrape only
4. Apify known-Reel scrape + screen recording
5. Apify scrape + manual comments/profile review
6. Optional: Apify scrape + transcript/on-screen-text extraction step if available or cheap

Do not assume the most complete scrape is the best. Score usefulness, reliability, cleanup burden, and cost together.

## Suggested Test Setup

Use 3–5 known Instagram Reels selected by the user:

- 1 weak/curiosity Reel
- 1 plausible tool/workflow Reel
- 1 promising claim with an external artifact
- 1 creator/account that may be repost/spam/affiliate-heavy if available
- Optional: 1 Reel already used in Intake for comparison

For each candidate scraper/workflow, capture:

- actor/scraper name
- public marketplace URL
- input settings
- run cost or estimated cost
- success/failure
- output fields returned
- cleanup needed
- whether raw output includes sensitive/private/signed URLs that should not be logged

## Scoring Criteria

Use the Framework standard's 0–2 scoring model:

- 0 = missing or unreliable
- 1 = partial / usable with cleanup
- 2 = clean and reliable

Score each candidate on:

| Criterion | Question |
|---|---|
| Known Reel URL support | Can it scrape a specific Reel URL directly? |
| Caption quality | Does it return full caption text cleanly? |
| Engagement fields | Does it return views, likes, comments, date, and other visible metrics? |
| Creator metadata | Does it return handle, bio, follower count, verification, or account context? |
| Comments | Can it return top comments or useful comment samples? |
| Media/transcript support | Does it help capture on-screen text, audio, thumbnails, or video metadata? |
| External links | Does it preserve mentioned links, profile links, or linked artifacts? |
| Cost per Reel | Is the cost acceptable for selective known-Reel Intake? |
| Reliability | Does it work consistently without fragile errors? |
| Export usability | Is output easy to paste into Intake or convert into the template? |
| Sanitization | Can raw/private/signed fields be excluded before repo logging? |

## Success Criteria

A strategy is successful if it can produce a useful Tier 1 bundle for a selected Reel with low cleanup and acceptable cost.

A strategy is a strong success if it can produce most Tier 2 legitimacy fields as well, especially creator metadata, engagement fields, comment signal, and external links.

A strategy should not be adopted if it is cheap but misses caption/source/creator data, or if it is complete but too expensive or fragile for repeated Intake use.

## Stop Conditions

Stop or down-rank a scraper if:

- it cannot reliably accept known Reel URLs
- it fails on ordinary public Reels
- it returns mostly signed/private media URLs instead of useful metadata
- cost per useful Reel becomes meaningfully higher than expected
- it requires too much manual cleanup for normal Intake
- it creates sanitization risk that is hard to remove

## Expected Output

Create a sanitized Incubator test file in `tests/` with:

- ranked candidate scrapers/workflows
- cost notes
- field coverage table
- example sanitized evidence bundle
- recommendation: replace screen recording, supplement it, or keep screen recording as primary
- suggested default Intake workflow
- unresolved questions

Possible filename:

`tests/2026-06-17_instagram_reel_scraper_intake_evidence_evaluation.md`

## Routing After Test

If successful:

- Update `MANIFEST.md` with the test result.
- Update the Framework standard if the evidence tiers need adjustment.
- Create a reusable Intake instruction for when to include scrape bundles.

If mixed:

- Keep screen recording as Tier 0.
- Adopt scraper only as optional Tier 2 enrichment.
- Document which fields are worth paying for.

If failed:

- Keep current screen recording workflow.
- Add a manual checklist for missing fields instead of adopting a paid scraper.
- Archive the scraper comparison as a rejected/Watchlist tool test.

## Sanitization Notes

Do not commit:

- raw scrape datasets
- signed/private Instagram media URLs
- cookies
- API keys
- account-specific tokens
- private user metadata
- unredacted raw scraper output

Commit only sanitized summaries, scoring tables, decisions, and reusable workflow recommendations.

## Suggested First Message for New Incubator Chat

This chat is a new Incubator chat for testing Instagram Reel scraper / Intake evidence workflows for The Lab. Please reference `Unl0ckedzERO/The-Lab`, especially:

- `MANIFEST.md`
- `framework/2026-06-17_instagram_reel_intake_evidence_standard.md`
- `handoffs/2026-06-17_framework_to_incubator_instagram_reel_scraper_intake_evidence_test.md`

Goal: compare Apify Instagram/Reels scrapers and/or hybrid workflows against the Framework evidence standard, using selected known Reel URLs, to determine whether a paid scrape bundle should supplement or replace the current screen-recording-only Intake workflow. Keep the test bounded, sanitized, and avoid committing raw scrape output.
