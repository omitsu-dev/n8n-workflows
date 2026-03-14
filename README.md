# n8n-workflows

Production-ready n8n workflow templates for common automation tasks. Import, configure credentials, and activate.

Built by the developer behind [32blog.com](https://32blog.com).

## Workflows

| Workflow | Trigger | Action | File |
|----------|---------|--------|------|
| **GitHub PR → Slack** | GitHub webhook (PR opened) | Sends rich Slack notification with PR details | [`github-pr-slack-notify.json`](workflows/github-pr-slack-notify.json) |
| **RSS → Slack** | Schedule (every 30 min) | Posts new RSS feed items to Slack channel | [`rss-to-slack.json`](workflows/rss-to-slack.json) |
| **Daily GitHub Summary** | Cron (weekdays 9 AM) | Summarizes open issues + PRs to Slack | [`daily-github-summary.json`](workflows/daily-github-summary.json) |
| **Webhook → Discord** | Generic webhook (POST) | Forwards any webhook payload as Discord embed | [`webhook-to-discord.json`](workflows/webhook-to-discord.json) |
| **Uptime Monitor** | Schedule (every 5 min) | Alerts Slack if site returns non-200 status | [`uptime-monitor.json`](workflows/uptime-monitor.json) |

## Quick Start

1. Open your n8n instance
2. **Add workflow** → **Import from file**
3. Select a `.json` file from `workflows/`
4. Replace `REPLACE_ME` credential IDs with your own
5. Activate the workflow

See [Setup Guide](docs/setup.md) for detailed credential configuration.

## Architecture

Each workflow follows this pattern:

```
Trigger → Filter/Transform → Action
```

- **Triggers**: Webhooks, scheduled cron, or polling
- **Filters**: Condition checks (e.g., only PR opened events, only non-200 responses)
- **Actions**: Slack messages, Discord embeds, HTTP requests

All workflows use n8n's built-in nodes — no custom nodes or external dependencies required.

## Customization

### Change notification channel

Edit the `channel` parameter in any Slack node:

```json
"channel": {
  "value": "#your-channel",
  "mode": "name"
}
```

### Change schedule interval

Edit the `interval` in any Schedule Trigger node:

```json
"rule": {
  "interval": [{ "field": "minutes", "minutesInterval": 15 }]
}
```

### Add more workflows

Export any workflow from n8n as JSON:
1. Open the workflow in n8n
2. **"..."** menu → **Download**
3. Save the `.json` file to `workflows/`

## Requirements

- n8n v1.30+ (self-hosted or cloud)
- Credentials for target services (Slack, GitHub, Discord)

## License

[MIT](LICENSE)
