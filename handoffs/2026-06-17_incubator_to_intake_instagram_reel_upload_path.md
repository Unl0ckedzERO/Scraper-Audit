# Handoff — Instagram Reel Upload Path for Intake

Date: 2026-06-17
Source Zone: Incubator
Target Zone: Intake
Item Type: Workflow / Scraper / Evidence Bundle
Status: Proven Upload Path

## Why This Passed Incubator

- The workflow improved on screen recording alone by preserving structured scrape data, media evidence, and transcript evidence in one upload-ready bundle.
- Multiple scraper candidates and toggle combinations were tested before choosing the lower-cost path.
- Local `whisper.cpp` transcription was tested against Apify's paid transcript toggle and was sufficient for Intake use.
- Bulk packaging was tested with multiple Reel sources and both audio/video variants.

## What Is Known

- Cheap Apify scrape outputs can expose usable media URLs without enabling paid transcript/video-download toggles.
- Downloaded media can be transcribed locally with `whisper.cpp large-v3-turbo`.
- The final local script creates upload-ready ZIPs containing:
  - media file,
  - local transcript,
  - matching Apify JSON export.
- The local folder structure is:
  - `Desktop/Raw Reels` — raw media and Apify JSON exports before processing.
  - `Desktop/Raw Reels/_processed` — processed source files.
  - `Desktop/Refined Reels` — upload-ready ZIP files.
  - `Desktop/Refined Reels/Refined Roots` — loose transcript/media/JSON support files.
- The script detects audio-only vs video media and names outputs accordingly.
- The script skips files when no matching JSON or multiple matching JSONs are found.

## What Is Unknown

- Whether the workflow remains frictionless across a larger variety of Instagram media URL formats.
- Whether future Instagram/CDN URL changes will affect media download reliability.
- Whether occasional Reels require paid transcription, manual review, or video-only/on-screen-text extraction.

## Intake Use Standard

For Instagram Reels selected for evidence review:

1. Run the chosen cheap scraper with transcript/download toggles off.
2. Download either audio-only or video media from the scraper-provided media URL.
3. Export the matching Apify JSON dataset item.
4. Place the media file and matching JSON export in `Desktop/Raw Reels`.
5. Run `transcribe_all.command`.
6. Upload the resulting `N-Reel.zip` bundle from `Desktop/Refined Reels` to the Intake chat.

## Intake Handling Guidance

- Use the ZIP bundle as the primary evidence upload.
- Treat the transcript as evidence, not final truth.
- Verify high-impact details such as money amounts, dates, names, product claims, and quantities against the media when they matter.
- Do not ask Intake to preserve or commit raw media, raw JSON, signed media URLs, or unredacted scrape output to GitHub.

## Routing After Adoption

- If the upload bundle is enough for first-pass audit, keep the item in Intake through Triage/Evidence Pass.
- If a Reel becomes a tool/workflow experiment, create a normal Intake-to-Incubator handoff using the ZIP as source evidence.
- If the local workflow itself needs revision, return to Incubator for a bounded workflow fix.
- If the workflow remains stable over several real Intake uses, promote a shorter quick-start to Framework.

## Sanitization Notes

Do not commit raw ZIP bundles, media files, signed/private URLs, API keys, credentials, unredacted Apify JSON, or full raw scrape output to The Lab repo. The repo should keep only sanitized summaries, decisions, handoffs, and workflow standards.
