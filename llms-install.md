# Installing the Heard MCP server (for AI agents)

This is a hosted server. Do not clone or build anything.

1. Ask the user for their Heard key. They get it by signing in at https://heard.dev/connect and clicking **Get my key**. It starts with `hgs_`. If they don't have a Heard account, they can sign up for free on the same page.
2. Add this server to the MCP settings, replacing `hgs_your_key` with their key:

```json
{
  "mcpServers": {
    "heard": {
      "type": "streamableHttp",
      "url": "https://api.heard.dev/v1/mcp/share",
      "headers": { "Authorization": "Bearer hgs_your_key" }
    }
  }
}
```

Some clients call the transport type `http` instead of `streamableHttp`. Use whichever your client expects.

3. Check it works by calling `heard_my_month`. It returns the user's agent hours this month. "No agent time in Heard yet this month" is a normal answer for a new account.

Never call `heard_invite_friend` with a `confirm_code` unless the user has seen the preview and said yes.
