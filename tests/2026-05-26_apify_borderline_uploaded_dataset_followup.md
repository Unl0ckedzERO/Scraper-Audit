# Apify Test — Uploaded Dataset Follow-up

Date: 2026-05-26  
Tool: Apify  
Actor: `borderline/indeed-scraper`  
Raw datasets stored: No — only sanitized summaries are committed.

## Files Reviewed

Two JSON datasets were uploaded for review:

1. `dataset_indeed-scraper_2026-05-27_03-18-13-327(1).json`
   - Appears to be the first 20-row `equipment operator` / Montana-style controlled test.
2. `dataset_indeed-scraper_2026-05-27_03-31-21-184.json`
   - Appears to be the second tighter `grader operator` / Montana-style test.

The third broad/blank-location test was discussed by cost and settings but was not included in the uploaded files at this point.

## Dataset 1 — 20-row Equipment Operator-style Search

Observed count: 20 records.

Field coverage:

- Job key: 20 / 20
- Title: 20 / 20
- Company/source: 20 / 20
- Location: 20 / 20
- Job URL: 20 / 20
- Apply URL: 16 / 20
- Description text: 20 / 20
- Date published: 20 / 20
- Age: 20 / 20
- Salary text: 15 / 20
- Job type: 20 / 20
- Benefits: 14 / 20
- Attributes: 20 / 20
- Requirements: 13 / 20

Assessment: Strong sheet-ready extraction. Some relevance drift exists, but output quality is much better than Parse Indeed.

## Dataset 2 — 5-row Grader/Operator-style Search

Observed count: 5 records.

Extracted rows:

| Title | Company | Location | Salary | Age |
|---|---|---|---|---|
| Heavy Equipment Technician | REIC | Belgrade, MT | $35 - $40 an hour | 5 days ago |
| General Equip Operator/Truck Driver | Westmoreland Mining LLC | Savage, MT | Not listed | 11 days ago |
| Asphalt Screed/Paver Operator | Advantage Asphalt Paving LLC | Missoula, MT | $30 - $36 an hour | 8 days ago |
| Lead Tech 1 | Colt Services | Billings, MT | Not listed | 14 days ago |
| Maintenance Technician | TGC Hospitality Management | Belgrade, MT | From $27 an hour | 11 hours ago |

Field coverage:

- Job key: 5 / 5
- Title: 5 / 5
- Company/source: 5 / 5
- Location: 5 / 5
- Job URL: 5 / 5
- Apply URL: 2 / 5
- Description text: 5 / 5
- Date published: 5 / 5
- Age: 5 / 5
- Salary text: 3 / 5
- Job type: 5 / 5
- Benefits: 3 / 5
- Attributes: 5 / 5
- Requirements: 1 / 5

Assessment: Very cost-efficient but lower recall and weaker precision for an exact `grader operator` lane. It captured adjacent equipment/mechanic/operator work, not many literal grader jobs.

## Cross-file Duplicate Check

One duplicated job key appeared across the two uploaded datasets:

- `1b294ddebef6101c` — General Equip Operator/Truck Driver, Westmoreland Mining LLC, Savage, MT

This confirms that cross-batch deduplication by `jobKey` should be part of the sheet pipeline.

## Workflow Update

Apify `borderline/indeed-scraper` remains the best tested Indeed extraction path.

Recommended default:

- Max rows: 100
- Max cost cap: $1
- Save only unique jobs: ON
- Include similar jobs: OFF for precision runs
- Include similar jobs: ON only for discovery/adjacent-role runs
- Deduplicate across runs by `jobKey`

## Next Practical Step

Define an Apify-to-Google-Sheets mapping and add a `Run ID`, `Search Query`, `Search Location`, `Run Cost`, and `jobKey` to every imported row so results from multiple runs can be deduplicated and traced.
