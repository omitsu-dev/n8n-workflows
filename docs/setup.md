# Setup Guide

## Prerequisites

- [n8n](https://n8n.io/) instance (self-hosted or n8n Cloud)
- API credentials for integrations (Slack, GitHub, Discord, etc.)

## Import a Workflow

1. Open your n8n instance
2. Click **"Add workflow"** → **"Import from file"**
3. Select a `.json` file from the `workflows/` directory
4. Update credential references (marked `REPLACE_ME`) with your own
5. Activate the workflow

## Credential Setup

### Slack

1. Create a Slack app at [api.slack.com/apps](https://api.slack.com/apps)
2. Add OAuth scopes: `chat:write`, `channels:read`
3. Install the app to your workspace
4. Copy the **Bot User OAuth Token**
5. In n8n: Settings → Credentials → Add **Slack API** credential

### GitHub

1. Go to [github.com/settings/tokens](https://github.com/settings/tokens)
2. Generate a **Fine-grained personal access token**
3. Select repos and permissions needed (Issues: read, Pull requests: read)
4. In n8n: Settings → Credentials → Add **GitHub API** credential

### Discord Webhook

1. In Discord: Server Settings → Integrations → Webhooks → New Webhook
2. Copy the webhook URL
3. Paste directly into the HTTP Request node URL field (no credential needed)

## Webhook Workflows

For workflows triggered by webhooks (GitHub PR, generic webhook):

1. After import, the webhook URL is shown in the Webhook node
2. Copy this URL and configure it in the source system
3. For GitHub: Repository → Settings → Webhooks → Add webhook
