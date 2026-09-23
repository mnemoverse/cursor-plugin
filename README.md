# Mnemoverse Memory for Cursor

Persistent memory for AI agents, shared across tools. One account gives Cursor the same long-term memory it has in Claude Code, VS Code, and any other MCP client: write a memory in one tool, recall it in another.

## What the plugin bundles

- **MCP server** (`mcp.json`): the hosted Mnemoverse server at `https://mcp.mnemoverse.com/mcp`. First use opens a browser sign-in (OAuth 2.1 with PKCE, Cursor's callback is supported); free tier at [console.mnemoverse.com](https://console.mnemoverse.com?utm_source=github&utm_medium=readme&utm_campaign=cursor-plugin), no credit card, no API key to paste.
- **Rule** (`rules/agent-memory-discipline.mdc`): recall before acting on project-specific work, save durable decisions and corrections afterwards, close superseded facts instead of overwriting them.
- **Skill** (`skills/agent-memory-discipline/`): the same discipline in full, published standalone as CC0 at [mnemoverse/agent-memory-discipline](https://github.com/mnemoverse/agent-memory-discipline).

## Tools

The documented remote tool surface includes `memory_read`, `memory_write`, `memory_list_recent`, `memory_stats`, `memory_feedback`, shared-room tools, and `vault_list` (secret aliases and metadata, not secret values). See the [current remote tool reference](https://mnemoverse.com/docs/api/remote-mcp-server) for the exposed surface.

Deletion is not an MCP tool on either the remote server or the current [local package](https://mnemoverse.com/docs/api/mcp-server); it is an administrative REST API operation. For a correction through MCP, write a fresh memory with `memory_write`; a corrective write alone does not establish that the older memory was superseded. The bundled rule describes the desired correction discipline, but it does not add a structured supersession tool: `supersedes`, `include_history`, and supersession-chain access are documented on the [REST API](https://mnemoverse.com/docs/api/reference), not exposed by this plugin's memory tools.

## Check your first cross-tool recall

After connecting and signing in, use a harmless fictional fact:

1. In Cursor, ask: "Use `memory_write` to save this in `project:cursor-plugin-demo`: The fictional Lantern demo serves its status page on port 7319." Check that the tool reports a successful write.
2. Open a fresh chat in another connected MCP client, signed in to the **same Mnemoverse account**. Ask: "Use `memory_read` in `project:cursor-plugin-demo`: Which port serves the Lantern demo's status page?"
3. Check that the tool result contains the saved fact. An answer from existing chat context alone does not verify cross-tool memory.

If recall is empty, check the account and exact domain, then confirm that the client actually called the tool. This checks saving and retrieval, not correction semantics or automatic recall on every future task. For the standing recall/save loop, see [Make Your Agent Use Memory](https://mnemoverse.com/docs/api/agent-memory).

## What gets stored

Only what you or the agent explicitly save through the memory tools. It does not record conversations and does not read chat history. Privacy policy: [mnemoverse.com/privacy](https://mnemoverse.com/privacy).

## Support

Issues in this repository, or [support@mnemoverse.com](mailto:support@mnemoverse.com).

The open-source MCP server package (MIT) lives at [mnemoverse/mcp-memory-server](https://github.com/mnemoverse/mcp-memory-server). A star there helps other builders find the project.

## License

Plugin: MIT. The bundled skill is CC0-1.0.
