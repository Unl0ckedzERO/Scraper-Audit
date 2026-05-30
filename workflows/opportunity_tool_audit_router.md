# Opportunity + Tool Audit Router

Date created: 2026-05-26  
Scope: Reels/business opportunity audit, tool audit, scraper/API workflow, and project handoff routing.

## Why This Exists

This chat began as an Instagram/Reels business opportunity audit and evolved into a broader testing space for tools, scrapers, APIs, and workflows that can support multiple projects. Without routing, serious ideas, hype content, tool experiments, and implementation work can blend together and reduce clarity.

This router keeps the chat useful as an intake/lab while preventing mature ideas from staying trapped in a noisy discovery thread.

## Recommended Structure

Use a hybrid model:

1. Keep this chat or a future project as an intake/lab for opportunity and tool audits.
2. Keep GitHub as the sanitized evidence/workflow ledger.
3. Move mature implementation work into the relevant project/chat.

Examples:

- Job-search implementation -> Job Search project
- Trading strategy/testing -> Trading project
- Resume/job-candidate workflows -> relevant resume project
- Tool/scraper evaluation -> Scraper Audit repo and audit chat/project
- Business opportunity experiments -> dedicated chat/project only after passing triage

## Intake Categories

Incoming items should be tagged as one or more of:

- Business opportunity
- Tool/workflow improvement
- Scraper/API/data-source candidate
- Creator/source to monitor
- Market signal / trend
- Content strategy idea
- Project-specific implementation idea
- Low-value/hype archive

## Routing Stages

### 1. Inbox

Capture the raw item with minimal interpretation.

Recommended fields:

- Source type: Reel, post, website, tool, API, marketplace, comment thread, video, transcript
- Link or attachment
- Creator/source
- Claimed idea
- User interest level
- Immediate context from user

### 2. Triage

Decide what kind of audit it needs.

Questions:

- Is the object itself promising, or is the creator/source promising?
- Is the claim about a business, a tool, a method, an audience, a workflow, or a market?
- Does it require scraping/research now, or can it be judged from supplied context?
- Is this relevant to a current project or a possible future project?

### 3. Evidence Pass

Only gather external evidence once the item passes initial usefulness.

Light evidence may include:

- transcript or screenshots
- landing page / pricing page scrape
- official docs
- marketplace listing
- public reviews or user reports

Deeper evidence may include:

- creator profile/authenticity check
- similar posts or competitor examples
- tool/API test
- pricing/unit economics
- search-volume or job-market style extraction
- project-specific implementation test

### 4. Audit

Evaluate the idea/tool using a stable rubric.

Suggested dimensions:

- practical utility
- fit with user/project priorities
- speed to test
- cost to test
- evidence quality
- workflow leverage
- downside/risk
- repeatability
- monetization or strategic value
- hype/clout signal quality

### 5. Route

Outcome categories:

- Reject / archive
- Pattern bank: weak alone, useful as part of a larger pattern
- Watchlist: promising source or trend, not actionable yet
- Tool stack: adopt/test as workflow support
- Project handoff: move into a specific project/chat
- Dedicated experiment: create a new chat/project/Git branch/sheet

## Reel-first vs Creator-first Baseline

Use a reel-first baseline when:

- one specific concept is being judged
- the creator is unknown
- the post makes a concrete claim
- quick usefulness screening is enough

Use a creator-first baseline when:

- multiple posts from the same creator seem useful
- authenticity, expertise, or repeated frameworks matter
- the creator may be a source of ongoing ideas
- the idea depends on trust in the creator's experience

Use both when:

- the reel is promising but the claim needs credibility support
- the creator sells a tool/course/service
- the idea may become a larger workflow or business experiment

## Scraping Rules

Do not scrape everything by default.

Use scraping only after an item crosses a usefulness threshold.

Recommended order:

1. User-provided transcript/screenshots first.
2. Firecrawl Scrape for public landing pages, docs, pricing pages, and tool pages.
3. Firecrawl Map for marketplace or site URL discovery.
4. Apify/Parse for structured extraction when a repeatable dataset is needed.
5. Avoid login/auth-heavy scraping unless the value justifies risk and cost.

## Clout / Hype Handling

Do not treat clout as proof, but do not ignore it.

Clout can mean:

- audience pain is real
- the topic is already pulling demand
- the framing is resonating
- the creator has distribution power

But clout can also mean:

- survivorship bias
- fake income claims
- affiliate incentives
- recycled guru content
- low implementation realism

Use the standard: `clout is a signal, not validation`.

## Personal Priority / Business DNA Inputs

A stable rubric should eventually include the user's priority list. Draft dimensions:

- low upfront cost
- fast proof-of-concept
- useful in real workflow
- automation/data leverage
- not HVAC-biased unless explicitly requested
- avoids overfitting to tentative ideas
- scalable learning value
- realistic implementation path
- low legal/platform risk
- can transition into a project, product, service, or repeatable process

## Main Concern

The biggest risk is scope blending: a noisy intake chat can start carrying implementation details that belong in specialized projects. The fix is not to split every idea immediately, but to route mature items once they pass triage.

## Recommended Operating Model

This chat/project should act as:

- intake
- triage
- evidence gathering
- early scoring
- tool evaluation
- handoff creation

It should not become the permanent home for:

- full job-search implementation
- trading strategy development
- resume project implementation
- mature business experiments
- raw data dumps

## Current Decision

Keep the broad audit/chat scope for now, but add routing discipline. Use GitHub for sanitized logs and workflows. Move implementation work into the target project as soon as a tool or idea becomes actionable.
