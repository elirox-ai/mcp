# Elirox Agent Kit

A skill for using **Elirox** from any AI agent (Claude Code, Codex, Cursor, OpenCode, …).
Connect your Elirox account and launch, stop, or manage CFD trading robots and trades — in natural
language, in your own language. You stay in control: every account-changing action is confirmed first.

## What you get

- **Onboarding by API key** — connect your Elirox account; connecting only reads the account, it never trades.
- **Robots** — launch and manage DCA / GRID / TradingView bots.
- **Trades** — open, modify (SL/TP, re-issue a pending order), and close orders.
- **Insight** — balance, plan limits and usage, assets, and a market overview.
- **Safety first** — conservative defaults and an explicit confirmation before anything that changes your account.

## Prerequisites

- An **Elirox account** (mobile or web app).
- An **Elirox API key**: in the Elirox app go to **Settings → Elirox Agent → API keys** and create one.
  The key is stored locally in your agent's own config and is sent only to Elirox.

## Install

Paste this **single message** to your agent:

```
npx skills add elirox-ai/mcp, connect Elirox
```

The agent installs the skill and immediately asks for your API key — no extra steps. Reply in your own
language (e.g. `npx skills add elirox-ai/mcp, connect Elirox`) and the agent will follow it.

## Per-agent setup (manual)

The one-line install above is the recommended path. If you'd rather register the MCP server yourself, add
the remote endpoint `https://app.elxapi.com/public/v1/mcp` to your agent and authenticate with
`Authorization: Bearer <your key>` via [`mcp-remote`](https://www.npmjs.com/package/mcp-remote). Replace
`KEY` with your API key.

**Claude Code**

```
claude mcp add-json --scope user elirox-mcp '{"type":"stdio","command":"npx","args":["-y","mcp-remote","https://app.elxapi.com/public/v1/mcp","--header","Authorization: Bearer KEY"]}'
```

**Codex** (`~/.codex/config.toml`)

```toml
[mcp_servers."elirox-mcp"]
command = "npx"
args = ["-y", "mcp-remote", "https://app.elxapi.com/public/v1/mcp", "--header", "Authorization: Bearer KEY"]
```

**Cursor** (`~/.cursor/mcp.json`)

```json
{ "mcpServers": { "elirox-mcp": { "command": "npx", "args": ["-y", "mcp-remote", "https://app.elxapi.com/public/v1/mcp", "--header", "Authorization: Bearer KEY"] } } }
```

**OpenCode** (`~/.config/opencode/config.json`)

```json
{ "mcp": { "servers": { "elirox-mcp": { "command": "npx", "args": ["-y", "mcp-remote", "https://app.elxapi.com/public/v1/mcp", "--header", "Authorization: Bearer KEY"] } } } }
```

## Tools

The `elirox-mcp` MCP server exposes read tools (account, active bots, assets, limits, last price,
TradingView webhook, opened/pending orders) and state-changing tools (launch DCA / GRID / TradingView
bots, stop a bot, create / modify / close / cancel orders). **Every state-changing tool requires an
explicit confirmation.** See [`SKILL.md`](./SKILL.md) for the full reference, parameters, and flows.

## Repo layout

```
mcp/
├── SKILL.md   # onboarding + bot-manager rules (the skill itself)
├── README.md  # this file
└── LICENSE    # MIT
```

## Version

**v1.0.0**

## License

[MIT](./LICENSE) © 2026 Elirox
