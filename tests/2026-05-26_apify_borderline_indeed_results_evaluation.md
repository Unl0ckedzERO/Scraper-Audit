# Apify Test — borderline/indeed-scraper Results Evaluation

Date: 2026-05-26  
Tool: Apify  
Actor: `borderline/indeed-scraper`  
Input target: `equipment operator` / Montana / full-time-style job search  
Downloaded result file: JSON dataset supplied by user  
Raw dataset stored: No — only sanitized summary and evaluation are committed.

## Result Summary

The actor returned 20 structured job records. This is a successful extraction test.

## Field Coverage

Observed field coverage across 20 records:

- Unique job keys: 20 / 20
- Job title: 20 / 20
- Company/source: 20 / 20
- Location object: 20 / 20
- Job URL: 20 / 20
- Apply URL: 16 / 20
- Description text: 20 / 20
- Date published: 20 / 20
- Age/relative posted date: 20 / 20
- Salary text: 15 / 20
- Job type: 20 / 20
- Expired: 0 / 20
- Remote: 0 / 20

## Example Extracted Rows

| Title | Company | Location | Salary | Age |
|---|---|---|---|---|
| Heavy Equipment Operator - Corvallis, MT | J & J Excavating & Trucking | Polson, MT | Not listed | 5 days ago |
| Equipment Operator/Laborer for Tree Service (CDL DRIVERS) | Treasure State Tree Service | Missoula, MT | $27 - $30 an hour | 5 days ago |
| Working Foreman | Turner Mining Group LLC | Corvallis, MT | Not listed | 5 days ago |
| Highway Maintenance Tech - CDL Driver / Equipment Operator - Deer Lodge | State of Montana | Deer Lodge, MT | $28.59 - $29.59 an hour | 7 days ago |
| General Equip Operator/Truck Driver | Westmoreland Mining LLC | Savage, MT | Not listed | 11 days ago |
| Sr. Project Manager, Architectural Millwork (Commercial Woodworking) | Provincial Store Fixtures | Big Sky, MT | $85,000 - $125,000 a year | 7 days ago |
| CERTIFIED WATER/WASTEWATER PLANT OPERATOR | City of Miles City | Miles City, MT | From $19.21 an hour | 12 days ago |
| Laborer - Excavation | Billings, MT Company | Billings, MT | $18 - $24 an hour | 11 days ago |
| Ready Mix Driver | Croell Inc. | Red Lodge, MT | $30 - $33 an hour | 12 days ago |
| Crusher Loader Operator | E&H Asphalt | Bozeman, MT | $30 - $35 an hour | 13 days ago |
| Crusher Loader Operator/Laborer | E&H Asphalt | Billings, MT | From $30 an hour | 13 days ago |
| Water Well Driller | Paramount Placement | Billings, MT | $75,000 - $90,000 a year | 10 hours ago |

## Quality Assessment

The output is substantially better than the Parse Indeed marketplace API for this use case.

Apify produced clean job records directly in one run, including job title, company, location, salary where available, date published, age, full description text, job URL, apply URL where available, benefits, occupations, attributes, and requirements.

## Strengths

- Clean row-level output
- Full descriptions included
- Salary extracted for most records
- Direct Indeed URLs included for all records
- Apply URLs included for most records
- Strong metadata depth: benefits, attributes, occupations, requirements, company links, ratings
- No need to call a separate detail endpoint per job

## Weaknesses / Cautions

- Some company names are inferred from `source` rather than `companyName` when companyName is missing.
- Some search relevance drift is present: examples include architectural millwork project manager, water/wastewater operator, drivers, and other adjacent roles.
- Need actual Apify cost used from run details to calculate value per clean row.
- Need to verify whether `max rows` and filters reliably prevent runaway runs.
- Need to determine whether output duplicates appear on larger runs.

## Comparison to Parse Indeed

Parse Indeed baseline:

- `search_jobs` returned counts, related queries, pagination, and job keys but not clean rows.
- `get_job_details` returned useful detail only one job key at a time.
- User confirmed Parse calls cost 2 credits each in this test series.

Apify borderline result:

- Returned 20 clean job records in a single run.
- No separate detail call needed per job.
- Much better suited for sheet population and job-search workflows.

## Verdict

Strong success. Keep `borderline/indeed-scraper` as the current best Indeed extraction candidate.

Provisional rating:

- Output quality: 9/10
- Sheet-readiness: 8/10
- Field richness: 9/10
- Relevance: 7/10
- Cost certainty: pending user-provided run cost
- Overall: Adopt for controlled tests, pending cost verification

## Next Steps

1. User should record actual run cost from Apify.
2. Test same actor with `Save only unique jobs` on and `View similar jobs` off if not already set.
3. Run one second small query with a more specific title, such as `grader operator` or `highway maintenance`, to evaluate precision.
4. If cost is acceptable, define a Google Sheets export mapping.
5. Compare one cheap alternative actor only if cost is too high.
