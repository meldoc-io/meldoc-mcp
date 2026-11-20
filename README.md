# Meldoc MCP server

The official [Model Context Protocol](https://modelcontextprotocol.io) server for [Meldoc](https://meldoc.io), the docs-as-code platform for engineering teams. It lets an AI agent search, read and edit your team's documentation — the documentation that lives in Git next to your code — with the same permissions you have in the web app.

The server is hosted. There is nothing to install or run: this repository holds its registry entry and the setup below.

| | |
| --- | --- |
| **URL** | `https://api.meldoc.io/mcp` |
| **Transport** | Streamable HTTP |
| **Auth** | OAuth 2.1 with dynamic client registration (sign in through the browser), or a Bearer integration token (`mdc_…`) |
| **Registry name** | `io.meldoc/mcp` |

## What an agent can do

- **Find and read**: full-text search, the document tree, a single document, related documents and the link graph between them, a document's history.
- **Write**: create and update documents, move them to Trash, attach assets, set custom fields — only where your role on the project allows it.
- **Collaborate**: list, add, reply to and resolve comments; manage the glossary and project contributors.
- **Check**: find duplicate documents and broken links; list workspaces, projects and templates.

The full list with parameters is in the [MCP tools reference](https://public.meldoc.io/meldoc/documentation/mcp-tools).

## Connect

The fastest way is the connect wizard in the app: **Integration Tokens → Connect an app → Connect an AI assistant**. It writes the setup for your client. The manual equivalents:

**Claude.ai and Claude Desktop** — **Settings → Connectors → Add custom connector**, URL `https://api.meldoc.io/mcp`, then **Allow** on the consent page.

**Claude Code**

```bash
claude mcp add --transport http meldoc https://api.meldoc.io/mcp
```

Then run `/mcp`, pick `meldoc` and choose **Authenticate**.

**Cursor, VS Code, Windsurf** — add to the client's MCP config (`.cursor/mcp.json`, `.vscode/mcp.json`, `.windsurf/mcp.json`):

```json
{
  "mcpServers": {
    "meldoc": {
      "type": "http",
      "url": "https://api.meldoc.io/mcp",
      "headers": { "Authorization": "Bearer mdc_your_token_here" }
    }
  }
}
```

Create the token in **Integration Tokens → Create token**; it is shown once.

**A client that can only start a local process** — bridge with [`mcp-remote`](https://www.npmjs.com/package/mcp-remote), which opens the browser to sign in:

```json
{
  "mcpServers": {
    "meldoc": { "command": "npx", "args": ["mcp-remote", "https://api.meldoc.io/mcp"] }
  }
}
```

If your account belongs to several workspaces, pin one with `?workspace=your-workspace` on the URL, or just ask the agent to "list my workspaces".

## Documentation

- [Getting started with MCP](https://public.meldoc.io/meldoc/documentation/mcp-getting-started)
- [Authentication](https://public.meldoc.io/meldoc/documentation/authentication)
- [MCP tools reference](https://public.meldoc.io/meldoc/documentation/mcp-tools)
- [Troubleshooting](https://public.meldoc.io/meldoc/documentation/mcp-troubleshooting)
- [meldoc.io/install/mcp](https://meldoc.io/install/mcp)

## Support

Open an issue in this repository.
