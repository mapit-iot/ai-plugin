# Mapit plugin for AI assistants

Official [Mapit](https://mapit.me) plugin. Ask your AI assistant about your own Mapit motorbike: account, vehicles, subscription, last reported location and route history. Everything is read-only.

> **Beta, free for now.** The My Mapit connector is a beta: it may change or stop working, it has no uptime promise, and Mapit does not charge for it today. Do not rely on it for emergencies or to recover a stolen bike: use the Mapit app. Use is subject to the [Mapit API Terms of Use](https://developers.mapit.me/terms) and [Privacy Notice](https://developers.mapit.me/privacy), for personal, non-commercial use.

## Contents

- **My Mapit connector** (`.mcp.json`): the remote MCP server at `https://api.mapit.me/mcp`. On first use you sign in with your Mapit account on the Mapit sign-in page and choose whether to share location and route history.
- **Skills** (`skills/`): `my-mapit` explains how to answer questions about your bike; `mapit-ride-summary` builds ride totals and logbooks with the Mapit app's own statistics rules.

## Install

**Claude Code**

```bash
/plugin marketplace add mapit-iot/ai-plugin
/plugin install mapit@mapit
```

Then run `/mcp`, choose **plugin:mapit:my-mapit** and sign in.

**OpenAI Codex**

```bash
codex plugin marketplace add mapit-iot/ai-plugin
codex plugin add mapit@mapit
```

**claude.ai or ChatGPT**: add a custom connector named **My Mapit** (Mi Mapit in Spanish) with the URL `https://api.mapit.me/mcp` and sign in with your Mapit account.

## Things to ask

- "Where is my bike?"
- "What rides did I do yesterday?"
- "How many km have I ridden this month?"
- "Show me the map of my last ride"
- "When does my subscription end?"

Answers always say when the location was last reported; the connector never shows live tracking.

## Privacy

The connector only reads the signed-in customer's own data. Location and route history need separate consent, and you can revoke a connection at any time at <https://login.mapit.me/connections>.
