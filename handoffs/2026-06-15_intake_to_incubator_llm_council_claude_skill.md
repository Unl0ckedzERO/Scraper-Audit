# Handoff: LLM Council / Claude Skill Pressure-Test

**Date:** 2026-06-15
**From:** Intake — Reels, Tools, Ideas
**To:** Incubator — Validated Ideas + Tool Tests
**Tags:** Tools, Workflow, Prompting, AI Evaluation
**Status:** Incubator candidate
**Recommended next action:** Run a small usefulness proof before adopting as a Lab process.

## One-line summary

A viral Instagram AI workflow idea points to an “LLM Council” pattern for reducing single-model agreement bias. The specific copied repo is a Claude Skill adaptation, not the original Karpathy multi-model app, but it may be more practical for lightweight Lab pressure-testing.

## Intake source summary

- Source type: Instagram Reel scrape from Intake.
- Public post URL: `https://www.instagram.com/p/DY3R56KFjX1/`
- Post date in scrape: 2026-05-28.
- Scrape date: 2026-05-30.
- Public engagement captured in scrape:
  - Comments: 36,074
  - Likes: 9,570
  - Views: 233,827
  - Plays: 450,926
- Caption claim: Claude/AI may agree with users too much; an “LLM Council” can pressure-test decisions using multiple advisor perspectives.
- Sanitization note: Raw comment data, commenter usernames, profile image URLs, signed media URLs, raw video/audio URLs, and raw JSON are intentionally not included here.

## Related repo under review

Copied/user repo:

`Unl0ckedzERO/claude-skills-llm-council`

Important clarification from Intake: this repo was not necessarily the exact repo shared by the scraped Reel. It came from a similar Reel/workflow and is being evaluated as a separate implementation candidate.

Repo summary:

- A Claude Skill called `llm-council`.
- Turns one decision/question into five advisor-style analyses plus a chairman verdict.
- Advisor roles:
  - Contrarian
  - First Principles Thinker
  - Expansionist
  - Outsider
  - Executor
- Trigger phrases include:
  - `council this`
  - `run the council`
  - `pressure-test this`
  - `stress-test this`
  - `war room this`
- Intended for meaningful decisions with tradeoffs, not simple factual lookups or routine generation tasks.

## Distinction from Karpathy LLM Council

Karpathy’s original `llm-council` concept is a multi-model local web app pattern:

1. Send a query to multiple LLMs.
2. Collect independent first opinions.
3. Have models anonymously review/rank each other.
4. Have a chairman model synthesize the final answer.

The Claude Skill implementation is lighter-weight and more convenient, but likely weaker because it simulates multiple perspectives inside Claude rather than using multiple truly independent models.

## Why this passed Intake

This item is worth moving because it matches a real Lab need: avoiding over-validation of seductive ideas, viral claims, tools, scrapers, and workflow opportunities.

The useful core is not the hype around the Reel. The useful core is the pressure-test pattern:

- Force downside analysis.
- Separate upside from execution feasibility.
- Catch assumptions and missing context.
- Produce a final route recommendation.
- Avoid default agreement with the user.

## Main risks / failure modes

1. **Fake disagreement:** One model may simulate disagreement without truly escaping its own bias.
2. **Persona theater:** The council could sound sophisticated while producing generic advice.
3. **False confidence:** A “chairman verdict” may feel more authoritative than it deserves.
4. **Overuse:** If applied to every Intake item, it will slow Intake down and overbuild weak ideas.
5. **Context mismatch:** The Claude Skill assumes Claude workspace/project context that may not map cleanly to ChatGPT/The Lab workflows.
6. **Attribution confusion:** Reel/source repo mismatch should stay documented so the implementation is not incorrectly treated as the exact shared asset.

## Incubator test plan

Run a small usefulness proof on 3–5 past or current Intake items.

Suggested test set:

1. A weak viral idea that should probably be archived.
2. A promising scraper/tool idea.
3. An ambiguous business/workflow idea.
4. Optional: an idea already routed correctly, to see whether the council adds anything.
5. Optional: a known false-positive/hype item.

For each item, compare normal Intake audit vs. Council Pass output.

Evaluation questions:

- Did the council catch a real risk the normal audit missed?
- Did it improve routing confidence?
- Did it create clearer next steps?
- Did it reduce sycophantic agreement?
- Did it waste time or add unnecessary polish?
- Did the final recommendation differ usefully from the first-pass audit?

## Proposed Incubator output

Create a short test note after running the proof:

`incubator/tests/llm-council-claude-skill-pressure-test.md`

Include:

- Test items used.
- Normal route decision.
- Council route decision.
- Differences observed.
- Whether the council changed the outcome.
- Recommendation: adopt, modify, watchlist, or archive.

## Possible later route

If useful:

- Move to Framework as an optional `Council Pass` rubric for promising but uncertain Intake items.
- Do not make it the default Intake format.

If not useful:

- Archive as a viral prompting pattern with limited practical value.

## Current route decision

**Move to Incubator.**

Do not implement broadly yet. Test as an optional pressure-test workflow for high-uncertainty, medium-stakes Intake items.
