# Google Sheets + Gmail

Automatically update a Google Sheet and send a Gmail notification when a new form or event arrives.

## What this workflow does

- Trigger automation with a defined event
- Process incoming data
- Route actions to the required app or service
- Save or notify the result

## Setup

1. Import the workflow JSON into n8n. 2. Connect your Google Sheets credential. 3. Connect your Gmail credential. 4. Map the row values to the message template.

## Production tips

- Store secrets in n8n credentials, not in the workflow JSON.
- Test with a small sample before enabling real automation.
- Add retry logic and error handling when integrating with external services.
