# Apify Test — Indeed Actor Shortlist

Date: 2026-05-26  
Search source: User-provided candidate links from Apify `indeed` search results  
Purpose: Shortlist the best Apify Indeed Actor candidates before spending credits.

## Initial Finding

The Apify search result set for `indeed` was too broad to evaluate directly. User provided a batch of Actor links, issue pages, API pages, input-schema pages, and related links. The useful step was to reduce those to direct Actor pages only.

## Strongest Candidates

### 1. borderline/indeed-scraper

URL: https://apify.com/borderline/indeed-scraper

Why shortlisted:

- Strongest trust signal among inspected options
- Rating: 4.8 from 28 reviews
- Total users: ~12K
- Monthly active users: ~1.7K
- Last modified: 5 days ago
- Issues response: ~0.92 hours
- Pricing: $5 / 1,000 jobs
- Claims detailed job listing output and rich fields

Likely best first real test despite not being the cheapest.

### 2. apivault_labs/indeed-jobs-scraper

URL: https://apify.com/apivault_labs/indeed-jobs-scraper

Why shortlisted:

- Cheapest inspected pay-per-result candidate
- Pricing: from $2 / 1,000 extracted jobs
- Last modified: 1 day ago
- Claims real-time scraping with title, company, salary, location, job type, description, posted date, company rating, and job URL
- Has maxPages and field toggles

Caution:

- Very low adoption at inspection time: 3 total users, 1 monthly active user, no reviews
- Best as a low-cost second test after a trusted baseline candidate

### 3. schnellscrapers/indeed-jobs-scraper

URL: https://apify.com/schnellscrapers/indeed-jobs-scraper

Why shortlisted:

- Pricing: from $2.99 / 1,000 results
- Last modified: 4 days ago
- Claims structured salary, location, posted date, snippet, apply URL, and full job description
- Mentions filters for job type, date, remote-only, radius, and search URLs

Caution:

- Very low adoption at inspection time: 2 total users, 1 monthly active user, no reviews

### 4. scrapemint/indeed-jobs-scraper

URL: https://apify.com/scrapemint/indeed-jobs-scraper

Why shortlisted:

- Claims robust enriched output including salary parsing, skills, seniority, remote/hybrid, Easy Apply, sponsored flag, and optional company enrichment
- Supports keywords, locations, search URLs, job IDs, company URLs, maxJobs, datePosted, jobType, radius, and splitByCity
- Pricing: $5 / 1,000 result items
- Last modified: 15 days ago

Caution:

- Low adoption at inspection time: 5 total users, 3 monthly active users, no reviews
- Richness may be overkill for the first simple test

## Deprioritized / Avoid for First Test

### apt_marble/indeed-jobs-scraper

URL: https://apify.com/apt_marble/indeed-jobs-scraper

Reason: marked deprecated.

### curious_coder/indeed-scraper

URL: https://apify.com/curious_coder/indeed-scraper

Reason: strong trust signals, but rental model is less appropriate for first test.

- Rating: 4.8 from 46 reviews
- Total users: ~3.7K
- Monthly active users: ~135
- Pricing: $20/month + usage

Better later if repeated use becomes likely.

### simpleapi/indeed-job-scraper

URL: https://apify.com/simpleapi/indeed-job-scraper

Reason: rental/subscription-style pricing and low visible adoption.

### orgupdate/indeed-jobs-scraper-api

URL: https://apify.com/orgupdate/indeed-jobs-scraper-api

Reason: $28/month + usage, low visible adoption, and not ideal for a low-cost proof test.

### scrapier/indeed-job-scraper

URL: https://apify.com/scrapier/indeed-job-scraper

Reason: $24.99/month + usage and low visible adoption.

## Recommended Test Order

1. First test: `borderline/indeed-scraper` for reliability baseline.
2. Second test if needed: `apivault_labs/indeed-jobs-scraper` for cheapest pay-per-result comparison.
3. Third test if needed: `schnellscrapers/indeed-jobs-scraper` or `scrapemint/indeed-jobs-scraper` depending on whether cost or enriched output matters more.

## Standard Test Query

Use the same query family already tested in Parse:

- query: equipment operator
- location: Montana
- job type: full-time, if supported
- posted within: 14 days, if supported
- max results: 10-20

## Success Criteria

A successful Apify actor should beat Parse Indeed by returning clean rows directly in one run:

- job title
- company
- location
- salary/pay, if available
- posted date or relative age
- job type
- job description or snippet
- direct job URL
- apply URL, if available
- source/search context

## Comparison Target

Parse Indeed current baseline:

- `search_jobs` is useful for volume, related queries, and job keys, but not clean rows.
- `get_job_details` returns useful data but costs too much at scale if called once per job.
- Apify wins if it returns clean job rows at a better cost and with reasonable reliability.
