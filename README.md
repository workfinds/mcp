# workfinds MCP server

Search open jobs from your AI assistant. [workfinds.app](https://workfinds.app) reads company career sites and
shows the jobs you can apply for from your country, remote, hybrid or onsite. This repository holds the connection
manifests for its public MCP server. The service itself is not in this repository.

- **Server address:** `https://workfinds.app/mcp` (Streamable HTTP)
- **Access:** free, read-only, no sign-in and no API key
- **Setup page:** <https://workfinds.app/mcp>
- **Privacy:** <https://workfinds.app/privacy> · **Terms:** <https://workfinds.app/terms> · **Support:** support@workfinds.app

## What it can do

Five read-only tools. Every result links to its page on workfinds.app.

| Tool | What it does |
|---|---|
| `search_jobs` | Search open jobs: words, the country you will work from, remote/hybrid/onsite, employment type, posting date, listed salary, role family |
| `get_job` | One job: place, work arrangement, employment type, pay when listed, when it was posted, whether it is still open, its apply link |
| `get_company` | One employer: open jobs, and its size, headquarters and website when known |
| `list_countries` | The country codes `search_jobs` accepts |
| `list_roles` | The role families `search_jobs` accepts |

Things to ask: "Find remote data engineer jobs I can apply for from the Philippines." · "Show hybrid marketing jobs in
Germany posted in the last 7 days that list a salary." · "Open the first result and tell me where to apply." ·
"Tell me about the company behind the first result."

## Connect

Use the server address above in any MCP client. The steps below follow each assistant's own documentation.

**Claude** (web, desktop, mobile): open Customize, then Connectors. Select Add, then Add custom connector. Name it
workfinds and paste the server address. Select Continue, choose No sign in, then Add. In a chat, open the plus menu,
then Connectors, and turn workfinds on.

**ChatGPT:** open Plugins. Select the plus button, then Add custom MCP server. Name it workfinds and paste the server
address under Connection. Set authentication to none, confirm the notice, then select Create as a plugin. Start a new
chat, type `@` and choose workfinds. Your account or workspace settings decide whether custom servers are allowed.

**Claude Code:**

```sh
claude mcp add --transport http workfinds https://workfinds.app/mcp
```

Then run `/mcp` to check the connection.

**Codex:** add to `~/.codex/config.toml`, then run `codex mcp list`:

```toml
[mcp_servers.workfinds]
url = "https://workfinds.app/mcp"
```

**Gemini CLI:**

```sh
gemini mcp add --transport http workfinds https://workfinds.app/mcp
```

Or install this repository as an extension: `gemini extensions install https://github.com/workfinds/mcp`.

**Cursor:** add `mcp.json` from this repository to `~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project):

```json
{
  "mcpServers": {
    "workfinds": { "url": "https://workfinds.app/mcp" }
  }
}
```

**Grok:** the Grok apps have no screen for adding an MCP server yet. Through the xAI API, add this to the `tools`
list of a request: `{"type": "mcp", "server_url": "https://workfinds.app/mcp", "server_label": "workfinds"}`.

**Any other client:** add a Streamable HTTP server named `workfinds` at the address above, with no authentication.

## Files

| File | For |
|---|---|
| `server.json` | The [MCP registry](https://registry.modelcontextprotocol.io) entry (`app.workfinds/jobs`) |
| `mcp.json`, `plugin.json` | A Cursor plugin (an Agent Plugin: the manifest plus the server entry) |
| `gemini-extension.json` | A Gemini CLI extension |
| `llms-install.md` | Setup text for an AI agent that installs the server for you |
| `assets/` | The icon (192, 400 and 512 px PNG) |

## Limits and fair use

Each address may make up to 500 searches and 2,000 job or company lookups a day, and up to 20 searches and 30 lookups a
minute. A search returns at most 50 jobs. Listings change, so confirm details on the employer's site before applying.

## License

MIT, see [LICENSE](LICENSE). It covers the files in this repository, not the workfinds.app service or its name and logo.
