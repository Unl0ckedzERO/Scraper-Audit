# Instagram Reel Scraper Test — Upload-Ready Intake Evidence Path

Date: 2026-06-17
Zone: Incubator
Tool or Source: Apify Instagram scrapers, scraper-provided media URLs, local `whisper.cpp`, local packaging script
Test Type: Scraper / Workflow / Intake Evidence
Raw Data Stored: No — only sanitized summary and evaluation are committed.

## Question

Can Instagram Reel evidence be captured for Intake more reliably than screen recording alone by using cheap scraper output, downloaded media, local transcription, and an upload-ready bundle?

## Setup

- Inputs: selected Instagram Reels already chosen for Lab Intake review.
- Scraper candidates tested:
  - Apify Instagram Reel Scraper
  - Apify Instagram Scraper
  - Instagram Scraper API competitor
- Baseline: screen recording plus optional manual notes.
- Transcript comparison: Apify built-in transcript toggle vs local `whisper.cpp` transcription from scraper-provided media.
- Packaging target: upload-ready ZIP bundles for Intake chats.
- Cost constraint: keep per-Reel processing cheap enough for selective Intake use, not large-scale scraping.

## Sanitized Observations

- Scraper-provided media URLs were sufficient to download usable audio-only and video files for tested Reels.
- `instagram-reel-scraper` transcript and video-download toggles were not needed by default because base scrape outputs still exposed usable media links.
- Local `whisper.cpp` using `large-v3-turbo` produced transcript quality close enough to Apify's paid transcript toggle for Intake use.
- One comparison showed `whisper.cpp` may preserve the literal phrasing better than the paid transcript when the speaker implied a value but did not explicitly say it.
- A local folder workflow was successfully built and tested:
  - `Desktop/Raw Reels` for raw downloaded media plus matching Apify JSON exports.
  - `Desktop/Refined Reels` for upload-ready ZIP bundles.
  - `Desktop/Refined Reels/Refined Roots` for loose supporting files.
  - `Desktop/Raw Reels/_processed` for processed source files.
- Bulk packaging was tested with multiple Reels, each represented by audio and video files plus Apify JSON exports.
- Output bundles correctly paired media, transcript, and matching Apify export when the raw media filename appeared in the Apify JSON.

## Field / Output Coverage

| Field / Output | Result | Notes |
|---|---|---|
| Source media | Present | Downloaded audio/video files from scraper-provided URLs worked in test. |
| Transcript | Present | Generated locally with `whisper.cpp`; quality sufficient for Intake evidence. |
| Apify JSON export | Present | Bundled as `N-ApifyExport.json`; raw export remains for Intake upload, not repo commit. |
| Upload package | Present | `N-Reel.zip` contains media, transcript, and Apify export. |
| Supporting loose files | Present | Stored under `Refined Reels/Refined Roots` to keep upload folder clean. |
| Processed source handling | Present | Raw files move to `_processed` after successful processing. |
| Bulk numbering | Present | Numbered bundle names prevent overwrites and preserve upload order. |
| Audio vs video distinction | Present | Script detects stream type and names outputs `Audio` or `Video`. |
| JSON-to-media matching | Present / guarded | Script searches JSON for raw media filename or stem; skips no-match or ambiguous-match cases. |
| Raw data committed to repo | No | Only this sanitized closeout is committed. |

## Evaluation

What worked:

- The paid Apify transcript/video toggles are not required as the default workflow.
- Cheap scraper runs plus local media download provide enough evidence for stronger Intake review than screen recording alone.
- Local `whisper.cpp` is a viable free transcript layer on the user's newer Apple Silicon MacBook Pro.
- The final folder/script workflow is user-friendly enough for repeat Intake use.
- The ZIP output path keeps Intake upload simple while preserving loose roots locally.

Remaining cautions:

- Raw Apify JSON exports, media files, signed CDN URLs, and full transcripts should not be committed to The Lab repo.
- JSON matching depends on preserving the raw downloaded media filename long enough for the script to find it inside the Apify export.
- If a media file does not match exactly one JSON export, the script should skip it rather than risk a wrong bundle.
- Transcripts should still be skimmed for money amounts, dates, names, and other high-impact claims.
- This workflow is designed for selected Reels, not broad Instagram scraping.

## Verdict

Tool Stack / Existing Project Handoff.

Adopt as the default upload path for Instagram Reel Intake evidence when a scrape is justified:

1. Run a cheap scraper with transcript/download toggles off.
2. Download returned audio or video media.
3. Place raw media plus matching Apify JSON export in `Raw Reels`.
4. Run local packaging script.
5. Upload resulting `N-Reel.zip` files to Intake.

## Route

Move from Incubator testing back to Intake as a proven evidence-ingestion workflow. Framework should treat this as the current preferred Reel evidence bundle path unless a future tool test replaces it.

## Next Step

Use this workflow in the next Intake Reel test. If it remains smooth in real Intake use, promote the workflow to a Framework operating note or Intake quick-start guide.

## Sanitization Notes

Do not commit raw media, raw Apify JSON, signed/private media links, API keys, credentials, unredacted API responses, full scrape outputs, or sensitive metadata. Commit only sanitized summaries, workflow decisions, and reusable implementation notes.
