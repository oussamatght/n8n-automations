# Data Cleaning

Clean incoming records, remove duplicates, and standardize values before saving or analyzing them.

## What this workflow does

- Trigger automation with a defined event
- Process incoming data
- Route actions to the required app or service
- Save or notify the result

## Setup

1. Import the workflow JSON. 2. Connect your source application or spreadsheet. 3. Configure the formatting or mapping logic. 4. Validate the cleaned output in the target sheet or database.

## Production tips

- Store secrets in n8n credentials, not in the workflow JSON.
- Test with a small sample before enabling real automation.
- Add retry logic and error handling when integrating with external services.
