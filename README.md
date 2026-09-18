# Mnemoverse Memory for Cursor

Persistent memory for AI agents, shared across tools. One account gives Cursor the same long-term memory it has in Claude Code, VS Code, and any other MCP client: write a memory in one tool, recall it in another.

## What the plugin bundles

- **MCP server** (`mcp.json`): the hosted Mnemoverse server at `https://mcp.mnemoverse.com/mcp`. First use opens a browser sign-in (OAuth 2.1 with PKCE, Cursor's callback is supported); free tier at [console.mnemoverse.com](https://console.mnemoverse.com?utm_source=github&utm_medium=readme&utm_campaign=cursor-plugin), no credit card, no API key to paste.
- **Rule** (`rules/agent-memory-discipline.mdc`): recall before acting on project-specific work, save durable decisions and corrections afterwards, close superseded facts instead of overwriting them.
- **Skill** (`skills/agent-memory-discipline/`): the same discipline in full, published standalone as CC0 at [mnemoverse/agent-memory-discipline](https://github.com/mnemoverse/agent-memory-discipline).

## Tools

Ten tools from the remote server: `memory_read`, `memory_write`, `memory_list_recent`, `memory_stats`, `memory_feedback`, four shared-room tools, and `vault_list` (aliases only). The two delete tools available in the [local package](https://mnemoverse.com/docs/api/mcp-server) are deliberately not exposed remotely, so a one-time sign-in can never wipe memory.

## What gets stored

Only what you or the agent explicitly save through the memory tools. It does not record conversations and does not read chat history. Privacy policy: [mnemoverse.com/privacy](https://mnemoverse.com/privacy).

## Support

Issues in this repository, or [helloworld@uinside.org](mailto:helloworld@uinside.org).

The open-source MCP server package (MIT) lives at [mnemoverse/mcp-memory-server](https://github.com/mnemoverse/mcp-memory-server). A star there helps other builders find the project.

## License

Plugin: MIT. The bundled skill is CC0-1.0.
