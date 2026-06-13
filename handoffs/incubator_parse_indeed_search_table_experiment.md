# Incubator Handoff — Parse Indeed Search Table Experiment

Date created: 2026-06-13  
Source context: Archive / prior mixed audit work  
Target chat: `Incubator — Validated Ideas + Tool Tests`  
Status: Promising tool/workflow experiment; not yet implementation-ready

## Why This Belongs in Incubator

The Indeed extraction work has already produced useful evidence:

- Parse's Indeed marketplace API can search Indeed and return search-level signals such as counts, related queries, pagination, and job keys.
- Parse's detail endpoint can return usable detail records for individual job keys.
- Apify's `borderline/indeed-scraper` currently produces cleaner row-level output and is the preferred implementation candidate for the Job Search project.

However, there is still a useful open question:

Can Parse's Indeed scraper/API be improved so a search call returns clean job-card rows suitable for a table, potentially making it cheaper or more flexible than Apify in the long run?

This is a good Incubator test because it is a validated idea with unresolved implementation value, but it does not yet belong in the Job Search project until the Parse workflow proves it can compete with Apify.

## Working Hypothesis

A revised Parse endpoint could return clean job-card rows directly from search results, or combine search plus limited details into a normalized response.

Potential endpoint concept:

`search_jobs_detailed`

Potential inputs:

- query
- location
- job type
- recency / days posted
- pagination start
- max results

Potential clean output fields:

- job key
- title
- company
- location
- salary / pay
- posted date or age
- job type
- snippet / summary
- direct job URL
- apply URL if available
- source

## Known Baseline From Prior Tests

### Parse baseline

Prior Parse testing found:

- `search_jobs` returned useful search-level data but not clean table rows.
- Search output included result counts, related query suggestions, pagination context, and job keys.
- `get_job_details` returned useful detail records when provided a job key.
- Each tested Parse endpoint call cost 2 credits/tokens.
- A search plus details for many jobs may become too expensive if every job requires a separate detail call.

### Apify baseline

Prior Apify testing found:

- `borderline/indeed-scraper` returned clean structured job rows in a single run.
- Output included title, company/source, location, salary where available, description, date/age, job URL, apply URL where available, and metadata.
- Apify is currently the stronger implementation candidate for the Job Search project.

## Incubator Test Goal

Determine whether Parse can be made competitive enough to justify further work.

The Incubator chat should not implement the final Job Search workflow. It should answer whether Parse is worth further revision/testing.

## Test Questions

1. Does Parse allow revising or creating a custom endpoint that returns clean search result rows?
2. Can the first search call produce title/company/location/salary/date/URL without needing one detail call per job?
3. If detail enrichment is required, can the endpoint limit detail calls to the first N jobs and still remain cost-effective?
4. Does Parse expose enough of the Indeed page state to extract clean visible job cards from `search_jobs`?
5. Would a public/canonical marketplace contribution be cheaper or reusable compared with a private revision?
6. How would expected Parse cost compare against Apify for 20, 50, and 100 clean rows?

## Success Criteria

Parse becomes worth further testing if it can plausibly deliver:

- one-call or low-call clean rows
- stable fields suitable for Google Sheets
- predictable cost lower than or competitive with Apify
- fewer relevance/noise problems than Apify, or some other clear advantage
- no need to commit raw responses, API keys, signed links, or sensitive metadata

## Failure Criteria

Archive or deprioritize the Parse branch if:

- clean rows require one detail call per job
- revision cost is high and no cheaper public/contribution path exists
- the endpoint cannot reliably extract visible job cards
- expected cost is worse than Apify
- output remains only useful for search-volume / job-key discovery

## Suggested Incubator First Pass

The Incubator chat should begin by reviewing the existing repo notes on:

- Parse Indeed pipeline assessment
- Parse Montana search and revision hypothesis
- Apify borderline Indeed results evaluation

Then produce a concise experiment plan:

1. What to check in Parse UI before spending credits.
2. What endpoint revision/request to ask Parse for.
3. What minimal test query to run.
4. What output table schema to require.
5. How to compare against Apify.
6. Whether this should remain Incubator, move to Job Search, or be archived.

## Boundaries

Do not:

- commit raw Parse/API responses
- include API keys or tokens
- paste private/signed links into GitHub
- turn this into the final Job Search implementation unless Parse passes the Incubator test
- overbuild a solution before confirming Parse can return clean rows affordably

## Expected Route After Incubator

Possible outcomes:

- **Archive / Pattern Bank:** Parse remains useful only as a discovery layer.
- **Tool Stack:** Parse becomes a selective market-sizing or job-key discovery tool.
- **Project Handoff:** If Parse can produce clean affordable rows, hand off to the Job Search project for implementation.
- **Dedicated Experiment:** If promising but technically uncertain, create a contained Parse revision experiment with cost limits.
