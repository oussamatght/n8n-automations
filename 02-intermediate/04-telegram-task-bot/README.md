# Telegram Task Bot

Create a Telegram bot that adds tasks, checks status, and sends follow-up reminders.

## What this workflow does

- Trigger automation with a defined event
- Process incoming data
- Route actions to the required app or service
- Save or notify the result

## Setup

1. Import the workflow JSON. 2. Create a Telegram bot and copy the API token. 3. Set up the bot command handlers and task storage. 4. Test sending and receiving task messages.

## Production tips

- Store secrets in n8n credentials, not in the workflow JSON.
- Test with a small sample before enabling real automation.
- Add retry logic and error handling when integrating with external services.
