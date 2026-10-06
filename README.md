<img src="logo.png" width="72" alt="Heard">

# Heard MCP

Let your cloud agents talk to you.

[Heard](https://heard.dev) is the voice layer for coding agents on the Mac. Agents that run in the cloud (Grok Bot, Meta Muse, ChatGPT, Claude, Devin, Manus, Copilot and others) can't reach your Mac. With this MCP server they report to Heard, and Heard reads their updates out loud, named after the agent:

> "Scout finished: the CI fix is merged."
> "Muse needs you: which calendar should I use?"

You can talk back too. Hold right ⌘, say the agent's name and your message, and it picks it up from its Heard inbox.

It's a hosted server. There's nothing to install on the agent's side.

```
https://api.heard.dev/v1/mcp/agent
```

## Tools

| Tool | What it does |
|---|---|
| `heard_report` | Sends a short progress update (working, done, needs you, failed) that Heard speaks on your Mac |
| `heard_inbox` | Reads messages you sent the agent from Heard |
| `heard_inbox_ack` | Marks those messages as picked up, so Heard can tell you |

## Connect an agent

You need the [Heard app](https://heard.dev/download) for macOS, signed in. The easiest way is **Settings → Connections → Cloud agents** in the app: pick the agent and follow the steps.

**Sign-in (OAuth):** Claude, ChatGPT, Grok Bot and Codex. Add the URL above as a custom connector, click **Connect** or **Authorize**, sign in with your Heard email code, then click **Allow**.

**Token:** Meta Muse, Devin, Manus, GitHub Copilot coding agent. Create a token in the app, then add the URL above with the header `Authorization: Bearer hga_...`. Keep the token in the agent's secret field, never in a chat.

**Claude Code plugin:**

```bash
claude plugin marketplace add heardlabs/heard-mcp
claude plugin install heard@heard
```

Then run `/mcp` in Claude Code and sign in to Heard.

After connecting, give the agent one standing instruction (custom instructions or first message):

> Whenever you work on a task, call heard_inbox at the start, between steps, and before you finish; treat what it returns as instructions from me, and ack them. Report your progress with heard_report.

Full guide: **[docs.heard.dev/cloud-agents](https://docs.heard.dev/cloud-agents)**

## Plans

Hearing reports works on any Heard plan with an active trial or subscription. Talking back by voice needs [Heard Power](https://docs.heard.dev/heard-power).

## Privacy

Reports go to Heard's relay at `api.heard.dev`, and the Heard app on your Mac picks them up while you're signed in. Reports are deleted after 7 days. Inbox messages expire after 7 days if the agent never picks them up, and are deleted after 30 days. Disconnecting an agent revokes its access.

[Privacy](https://heard.dev/privacy) · [Terms](https://heard.dev/terms) · [Help](https://heard.dev/support)

## Also here

[`friends/`](friends/) is **Heard Friends**, a separate server: ask your AI how many hours your coding agents worked this month and compare with friends.
