# Apify Test — Dataset Share Link Access

Date: 2026-05-26  
Tool: Apify  
Actor under test: `borderline/indeed-scraper`  
Dataset access method tested: signed/shareable Apify dataset items URL  
Raw URL stored: No — signed dataset URLs should not be committed.

## Result

The signed Apify dataset URL could not be fetched from ChatGPT's web access path. The fetch returned a cache/fetch failure rather than the JSON dataset items.

## Security Note

Signed dataset URLs include a signature/token-like query parameter and should be treated as semi-sensitive. Do not commit the raw full URL to GitHub. Log only that a signed dataset link was tested.

## Workflow Implication

For Apify result review, the best next options are:

1. Download the dataset as JSON or CSV and upload it directly to the chat.
2. Copy/paste a small clean sample of rows.
3. Export the dataset and store a sanitized summary in GitHub, not the raw signed URL.

## Next Step

User should upload the downloaded JSON/CSV results or paste a sample. The analysis should compare Apify output against Parse Indeed:

- row cleanliness
- fields returned
- cost used
- number of rows
- direct URL availability
- salary/pay availability
- whether output is sheet-ready
