# AI Email Classifier

Classify emails with AI, assign labels, and trigger follow-ups for different categories.

## What this workflow does

- Trigger automation with a defined event
- Process incoming data
- Route actions to the required app or service
- Save or notify the result

## Setup

1. Import the workflow JSON. 2. Connect your email account and AI model provider. 3. Define your classification labels. 4. Route each email to the correct process.

## Production tips

- Store secrets in n8n credentials, not in the workflow JSON.
- Test with a small sample before enabling real automation.
- Add retry logic and error handling when integrating with external services.
