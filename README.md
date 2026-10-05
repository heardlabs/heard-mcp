<img src="logo.png" width="72" alt="Heard">

# Heard MCP

Ask your AI assistant how many hours your coding agents worked this month.

[Heard](https://heard.dev) is the voice layer for coding agents on the Mac. It reads Claude Code and Codex out loud while they work. It also keeps one number per month: how long your agents were busy. This MCP server lets Claude, ChatGPT, Codex, Cursor and other assistants read that number, show your board next to your friends, and send an invite when you ask for one.

It's a hosted server. There's nothing to install or run.

```
https://api.heard.dev/v1/mcp/share
```

## Things to ask

- "How many hours did my coding agents work this month?"
- "Where am I on my Heard board?"
- "Write a short post about my month with my invite link."
- "Invite sam@example.com to Heard."

## Tools

| Tool | What it does | Changes anything? |
|---|---|---|
| `heard_my_month` | Your agent hours this month and your rank among friends | No |
| `heard_share_card` | A ready-to-paste line with your hours and invite link | No |
| `heard_compare` | You and your friends, ranked by agent hours | No |
| `heard_invite_friend` | Emails one friend an invite. The first call only shows a preview. It sends after you say yes. Max 5 a day. | Yes, sends one email |

## Set it up

1. Sign in at **[heard.dev/connect](https://heard.dev/connect)** and click **Get my key**. The page gives you the exact line for each app, key included.
2. Paste it into your assistant.

**Claude Code**

```bash
claude mcp add --transport http heard https://api.heard.dev/v1/mcp/share \
  --header "Authorization: Bearer $HEARD_KEY"
```

Or as a plugin:

```bash
claude plugin marketplace add heardlabs/heard-mcp
claude plugin install heard@heard
```

The plugin reads your key from the `HEARD_KEY` environment variable.

**Codex** (`~/.codex/config.toml`)

```toml
[mcp_servers.heard]
url = "https://api.heard.dev/v1/mcp/share"
bearer_token_env_var = "HEARD_KEY"
```

**Cursor and other apps** (`mcp.json`)

```json
{
  "mcpServers": {
    "heard": {
      "type": "http",
      "url": "https://api.heard.dev/v1/mcp/share",
      "headers": { "Authorization": "Bearer hgs_your_key" }
    }
  }
}
```

**Claude.ai, ChatGPT, Grok, Meta Muse:** add a custom connector with the URL above and an `Authorization: Bearer <key>` header. One-click sign-in for these apps is coming. It won't need a key.

## What the assistant can see

Your first name, your agent hours for the month, your rank on your board, and your invite link. That's it. Heard counts hours from the timestamps Claude Code and Codex save on your Mac. It never reads your prompts or your code, and none of that reaches this server. Friends only show up if they chose to share their hours.

Turn your key off any time at [heard.dev/connect](https://heard.dev/connect). Getting a new key also turns off the old one.

[Privacy](https://heard.dev/privacy) · [Terms](https://heard.dev/terms) · [Help](https://heard.dev/support) · [Docs](https://docs.heard.dev)
