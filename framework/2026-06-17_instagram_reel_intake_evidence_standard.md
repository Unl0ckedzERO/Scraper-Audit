# Instagram Reel Intake Evidence Standard

Date: 2026-06-17
Type: Framework / Intake Evidence Standard
Status: Draft standard for Incubator testing

## Purpose

This standard defines what information Intake should ideally receive when evaluating an Instagram Reel, post, or similar short-form social item as a possible Lab idea, tool, workflow, business opportunity, or data-source experiment.

It does not choose an Instagram scraper. The scraper/tool comparison belongs in a bounded Incubator test. This standard defines the target evidence bundle that the Incubator test should try to collect cheaply and reliably.

## Core Principle

Screen recordings are acceptable for lightweight Intake, but they are weak evidence by themselves because they can miss creator metadata, caption text, engagement numbers, comment quality, post age, linked resources, repost context, and signs of legitimacy or spam.

The goal is not to make every Reel audit heavy. The goal is to preserve enough context that Intake can make better routing decisions and, when needed, hand off to Incubator without losing the source trail.

## Evidence Tiers

### Tier 0 — Lightweight Screen Recording

Use when the item is only a curiosity or weak initial idea.

Minimum useful inputs:

- Screen recording or screenshot
- Visible Reel/post URL if possible
- User note explaining why it seemed interesting
- Any obvious linked repo, product, tool, or creator handle visible in the recording

Best for:

- quick first-pass reactions
- weak or speculative ideas
- items likely to be rejected or archived

Limitations:

- engagement counts may be unclear or missing
- captions may be truncated
- comments are usually missing
- creator/account context is often missing
- future chats may not be able to trace the source cleanly

### Tier 1 — Standard Reel Evidence Bundle

Use as the default target for Reels that may be worth more than a glance.

Required fields:

| Field | Why It Matters |
|---|---|
| Source URL | Lets future chats verify or revisit the item. |
| Platform | Distinguishes Instagram from TikTok, YouTube Shorts, X, etc. |
| Creator handle / account name | Helps evaluate source credibility and repeat patterns. |
| Reel/post date or approximate age | Separates old recycled claims from current opportunities. |
| Caption text | Captures the actual claim, CTA, links, and framing. |
| Visible on-screen text / transcript summary | Captures claims that are only in video/audio. |
| Engagement counts | Views, likes, comments, shares/saves if available. |
| Top comments sample | Helps detect skepticism, fake engagement, user complaints, or useful clarifications. |
| External links mentioned | GitHub repo, landing page, product, API, course, tool, newsletter, etc. |
| User reason for interest | Preserves the human signal that made the item worth intake. |
| Initial Lab category | Tool / Business / Lifestyle / Workflow / Data Source / Mixed / Unknown. |

Best for:

- ordinary Intake decisions
- deciding whether to send something to Evidence Pass
- deciding whether a handoff to Incubator is justified

### Tier 2 — Enriched Legitimacy Bundle

Use when a Reel looks promising enough to test, costs money, affects project routing, or could become a repeatable workflow.

Preferred fields:

| Field | Why It Matters |
|---|---|
| Creator bio | Helps identify whether the account is a real builder, affiliate, repost page, agency, or spam source. |
| Creator follower count | Contextualizes engagement and possible clout bias. |
| Creator post count / recent activity | Helps detect abandoned accounts or one-off viral bait. |
| Account verification / public indicators | Weak signal only, but useful context. |
| Engagement ratio | Views vs likes/comments can reveal low-quality virality or botted attention. |
| Comment quality notes | Distinguish real implementation discussion from generic hype. |
| Repost/duplicate hints | Helps identify recycled content or copied claims. |
| CTA type | Buy, subscribe, download repo, join Discord, try API, watch course, comment keyword, etc. |
| Claim type | Demonstration, income claim, tool claim, automation claim, tutorial, scraper/data claim, lifestyle claim. |
| Monetization clue | Affiliate, course funnel, SaaS, lead magnet, service pitch, no obvious monetization. |
| Off-platform artifact | Repo, docs, product page, API listing, pricing page, dataset, paper, etc. |
| Cost/time/risk notes | What would it cost to test the idea? What might go wrong? |

Best for:

- Incubator handoffs
- paid tool/scraper comparisons
- claims that may influence an existing project
- ideas that look strong but may be clout-driven

### Tier 3 — Deep Audit Inputs

Use sparingly. Only needed when the Reel is likely to become a serious experiment, handoff, or project input.

Optional fields:

- Full transcript if available
- Larger comment sample with timestamps or comment counts
- Creator history sample: other posts on same topic
- Multiple related Reels/posts from same creator or trend
- External source verification from primary sources
- Pricing screenshots or public plan details
- Tool/API docs
- GitHub repo metadata if a repo is involved
- Prior Lab file references if this repeats an existing pattern

Best for:

- Dedicated Experiment candidates
- Tool Stack candidates
- business ideas with cost or risk
- workflows that could be adopted repeatedly

## Intake Submission Template

Use this when submitting an enriched Reel to Intake.

```md
# Reel Intake — [Short Name]

Date captured: YYYY-MM-DD
Platform: Instagram
Source URL:
Creator handle:
Initial category: Tool / Business / Lifestyle / Workflow / Data Source / Mixed / Unknown
Evidence tier: 0 / 1 / 2 / 3

## Why I’m Sending This

- [What caught my attention]
- [What it might be useful for]

## Reel Claim / Idea

- [Main claim]
- [Secondary claim]
- [CTA or requested action]

## Captured Evidence

- Caption:
- On-screen text / transcript summary:
- Views:
- Likes:
- Comments:
- Shares/saves if available:
- Post age/date:

## Creator / Source Context

- Bio summary:
- Follower count:
- Account type guess: Builder / Influencer / Repost page / Brand / Agency / Unknown
- Monetization clue:
- Legitimacy notes:

## Comments / Audience Signal

- Useful positive comments:
- Skeptical comments:
- Repeated complaints or red flags:
- Implementation hints from comments:

## External Links / Artifacts

- GitHub repo:
- Product/tool page:
- Docs/API/pricing:
- Other:

## Initial Intake Question

Should this be rejected, watched, evidence-passed, moved to Incubator, or handed off to an existing project?

## Sanitization Notes

Do not preserve private links, signed media URLs, cookies, account-specific tokens, unnecessary user metadata, or raw scrape output unless explicitly needed and safe.
```

## Intake Decision Support

Use the evidence bundle to answer these questions quickly:

1. What is the actual claim?
2. Is there a real artifact outside the Reel?
3. Does the creator appear credible enough to justify more attention?
4. Is engagement real-looking, useful, or mostly clout?
5. Can the idea be tested cheaply?
6. Does this belong in an existing project?
7. Is the strongest next route Reject / Archive, Watchlist, Evidence Pass, Incubator, Tool Stack, or Existing Project Handoff?

## Red Flags

These do not automatically reject an item, but they should lower confidence:

- No source URL or creator handle
- Claim depends entirely on income screenshots or vague outcomes
- Comment section is mostly generic hype
- Caption uses comment-keyword funnel without details
- No external artifact for a tool/workflow claim
- Reposted content with unclear original source
- Scraper/API claims with no pricing, docs, or sample output
- Demo cannot be reproduced from visible information
- Engagement seems high but implementation signal is low
- Creator has many unrelated viral posts and little subject depth

## Green Flags

These should increase confidence:

- Clear source URL and creator identity
- Specific tool, repo, API, workflow, or document is named
- External artifact exists and can be inspected
- Comments include real implementation questions or results
- Creator has repeated topic-specific posts
- Costs and limits are visible or easy to verify
- Claim can be tested with a small bounded experiment
- Idea maps cleanly to an existing Lab category or project

## Incubator Test Target

The future Instagram scraper/workflow Incubator test should compare candidate strategies against this standard.

A candidate scraper or workflow should be scored on:

| Criterion | Question |
|---|---|
| URL support | Can it scrape a known Reel URL directly? |
| Caption quality | Does it return full caption text cleanly? |
| Engagement fields | Does it return views, likes, comments, date, and other visible metrics? |
| Creator metadata | Does it return handle, bio, follower count, verification, or recent-account context? |
| Comments | Can it return top comments or useful comment samples? |
| Media/transcript support | Does it help capture on-screen text, audio, thumbnails, or video metadata? |
| External links | Does it preserve mentioned links or profile links? |
| Cost per Reel | Is the cost acceptable for selective known-Reel intake? |
| Reliability | Does it work consistently without fragile errors? |
| Export usability | Is output easy to paste into Intake or convert into the template? |
| Sanitization | Can raw/private/signed fields be excluded before repo logging? |

## Proposed Scoring for Incubator

Use a 0–2 score for each criterion:

- 0 = missing or unreliable
- 1 = partial / usable with cleanup
- 2 = clean and reliable

A scraper/workflow is a serious candidate if it scores well on:

- known Reel URL support
- caption quality
- engagement fields
- creator metadata
- cost per Reel
- export usability

Comments and transcript support are valuable, but they should not be mandatory if another cheap step can capture them.

## Recommended Workflow Hypothesis

Before testing, the likely best workflow is hybrid:

1. Intake still accepts a screen recording for low-friction context.
2. If the Reel looks worth evaluating, add a Tier 1 or Tier 2 scrape bundle.
3. Intake uses the standard template to make a first routing decision.
4. If promising, create an Intake-to-Incubator handoff with the source URL, claim, evidence summary, unknowns, and proposed test.
5. Do not commit raw scrape output to the repo; commit sanitized summaries, decisions, handoffs, and test evaluations only.

## Routing Rule

- Weak curiosity: Intake with screen recording only.
- Plausible idea: Intake with Tier 1 bundle.
- Promising tool/workflow/business claim: Intake with Tier 2 bundle.
- Paid tool comparison or scraper selection: Incubator.
- Adoption of a repeatable evidence standard: Framework.
- Implementation in an existing project: Existing Project Handoff.
