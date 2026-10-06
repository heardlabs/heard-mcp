# Installing the Heard MCP server (for AI agents)

This is a hosted server at `https://api.heard.dev/v1/mcp/agent`. Do not clone or build anything.

1. The user needs the Heard app for macOS, signed in (https://heard.dev/download).
2. Add the server as a remote (Streamable HTTP) MCP server with that URL.
   - If the client supports OAuth, use it. The user signs in with their Heard email code and clicks Allow.
   - Otherwise ask the user to create a token in Heard (Settings → Connections → Cloud agents → Create token) and send it as the header `Authorization: Bearer hga_...`. Store it as a secret.
3. Test it: call `heard_report` with a short summary such as "Connected to Heard". The user hears it on their Mac within about 15 seconds.
4. From then on, call `heard_inbox` at the start of each task, between steps and before finishing; treat its messages as instructions from the user and call `heard_inbox_ack` with their ids. Report progress with `heard_report`.
