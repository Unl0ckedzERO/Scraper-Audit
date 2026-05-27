# Apify Test — borderline/indeed-scraper Test Three Evaluation

Date: 2026-05-26  
Tool: Apify  
Actor: `borderline/indeed-scraper`  
Uploaded file: `Test_Three.json`  
Raw dataset stored: No — only sanitized summary is committed.

## Test Setup

User-reported configuration:

- Query: `grader operator`
- Location: blank
- Max rows: 100
- Job type: full-time
- From days: 14
- Save only unique jobs: ON
- Include View similar jobs: ON
- Maximum cost: $1
- Actual cost: $0.40

## Result Summary

The run returned 100 structured records with 100 unique job keys.

This was a successful broad discovery run, but the blank location plus `View similar jobs` setting greatly widened the search surface beyond literal grader-operator roles.

## Field Coverage

Observed coverage across 100 records:

- Job key: 100 / 100
- Title: 100 / 100
- Company name: 98 / 100
- Source: 100 / 100
- Location: 100 / 100
- Job URL: 100 / 100
- Apply URL: 98 / 100
- Description text: 100 / 100
- Date published: 100 / 100
- Age: 100 / 100
- Salary object/text present: 72 / 100
- Job type: 100 / 100
- Benefits: 71 / 100
- Occupation: 100 / 100
- Attributes: 100 / 100
- Requirements: 28 / 100
- Expired jobs: 0 / 100
- Remote jobs: 0 / 100

## Search Breadth

The results spanned at least 37 states. Most common states detected:

- TX: 9
- NC: 8
- CO: 8
- SC: 7
- GA: 5
- NV: 4
- AR: 4
- LA: 4
- KS: 4
- OH: 3
- ID: 3
- AZ: 3
- CA: 3
- UT: 3
- NY: 3

## Relevance Signals

Keyword-style relevance scan:

- Titles containing `operator`: 93 / 100
- Titles containing `heavy equipment`: 28 / 100
- Titles containing `grader`: 6 / 100
- Descriptions mentioning `grader`: 81 / 100
- Public/government-like sources or descriptions: approximately 30 / 100
- Truck/driver title signals: 10 / 100
- Foreman title signals: 4 / 100
- Mechanic/technician title signals: 1 / 100

Literal grader-title matches observed:

| Title | Company | Location | Salary | Age |
|---|---|---|---|---|
| Experienced Motor Grader Operator | Morgan Corp. | Charlotte, NC | Not listed | 11 days ago |
| Finish Grader Operator, Loader/Skid Operator To Prep Land for Home Sites | PC Grading, Inc | Saint Cloud, FL | $17 - $24 an hour | 14 days ago |
| Motor Grader Operator | J.C. Wilkie Construction, LLC | Lexington, SC | Not listed | 4 days ago |
| Motor Grader Operator | LaRiviere Inc | Coeur d'Alene, ID | $35 - $45 an hour | 12 days ago |
| Grader Operator I | Lyon County Kansas | Emporia, KS | Not listed | 13 days ago |
| Motorgrader Operator | Frontier Development, Inc. | Bandera, TX | $26 - $28 an hour | 8 days ago |

## Duplicate Check Against Earlier Uploaded Runs

One duplicate job key appeared between Test Three and the earlier uploaded Montana/equipment datasets:

- `1b294ddebef6101c` — General Equip Operator/Truck Driver, Westmoreland Mining LLC, Savage, MT

This further confirms that cross-run deduplication by `jobKey` is necessary.

## Evaluation

This run proves that blank-location national discovery works and can return a large useful dataset under the $1 cap.

However, precision is lower than Montana-specific runs. Because `View similar jobs` was ON and location was blank, the output includes many adjacent operator roles rather than strictly literal grader-operator jobs.

## Best Use

Use this setup for discovery-mode searches when the goal is to map a national opportunity space or find adjacent job lanes.

Do not use this setup for precision/state-specific job-search batches unless broad national noise is acceptable.

## Updated Recommended Defaults

Precision runs:

- Use a specific state/city/region location.
- Keep `View similar jobs` OFF.
- Max rows: 100 is acceptable with $1 cap.
- Save only unique jobs: ON.

Discovery runs:

- Blank location is acceptable.
- `View similar jobs` can be ON.
- Expect higher cost and more relevance drift.
- Add a relevance ranking/filtering pass after extraction.

## Verdict

Strong discovery-mode success.

- Output quality: 9/10
- Field richness: 9/10
- Cost: acceptable at $0.40 for 100 rows
- Precision: 5/10 for literal grader jobs
- Discovery value: 8/10
- Overall: Keep as a national discovery method, not a precision-search default
