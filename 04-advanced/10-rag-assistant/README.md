# RAG Assistant

Search your internal documents and answer questions grounded in company knowledge.

## What this workflow does

- Trigger automation with a defined event
- Process incoming data
- Route actions to the required app or service
- Save or notify the result

## Setup

1. Import the workflow JSON. 2. Connect your document source and embedding model. 3. Configure the retrieval and prompt logic. 4. Expose the assistant via chat or API.

## Production tips

- Store secrets in n8n credentials, not in the workflow JSON.
- Test with a small sample before enabling real automation.
- Add retry logic and error handling when integrating with external services.
