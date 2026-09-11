# Weather Automation

Fetch weather data, compare with conditions, and send push or email alerts when thresholds are hit.

## What this workflow does

- Trigger automation with a defined event
- Process incoming data
- Route actions to the required app or service
- Save or notify the result

## Setup

1. Import the workflow JSON. 2. Add a weather API key. 3. Define trigger thresholds. 4. Link your preferred notification destination.

## Production tips

- Store secrets in n8n credentials, not in the workflow JSON.
- Test with a small sample before enabling real automation.
- Add retry logic and error handling when integrating with external services.
