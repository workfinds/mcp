# workfinds.app MCP server

Search open jobs from your AI assistant. [workfinds.app](https://workfinds.app) is a free job search site and app that
lists open jobs taken straight from employers' own career sites and hiring systems, so every job links to the real
posting and you apply on the employer's own page. This repository holds the connection files for its public MCP
server. The service itself is not in this repository.

- **Server address:** `https://workfinds.app/mcp` (Streamable HTTP)
- **Access:** free, read-only, no sign-in and no API key
- **Setup page:** <https://workfinds.app/mcp>
- **ChatGPT plugin:** <https://chatgpt.com/plugins/plugin_asdk_app_6af5a671610c8191aacf3a15581b31ce>
- **Privacy:** <https://workfinds.app/privacy> · **Terms:** <https://workfinds.app/terms> · **Support:** support@workfinds.app

## About workfinds

- **Only open jobs, linked to the employer's own posting.** Closed jobs are taken down. workfinds never applies for you.
- **Jobs you can apply for from your country.** Filter by the country you can work from, remote, hybrid or onsite,
  employment type, posting date and listed salary. Place, work arrangement and pay are shown as the employer
  published them.
- **No ads and no third-party trackers.** Results are ordered by relevance and recency, never by payment.
- **No AI mass auto-apply.** We don't add to the flood of job applications.
- **Countries:** jobs in more than 100 countries, the most in the United States, Germany, Brazil, the United
  Kingdom, France, Japan, Canada, India, Singapore and Spain.
- **Languages:** the site and the apps come in 31 interface languages. Job text stays in the language the employer
  wrote it in.
- **Apps:** the iOS app is on the [App Store](https://apps.apple.com/app/id6826945980). The Android app is in closed
  testing on Google Play, and [workfinds.app](https://workfinds.app) shows its current status.

## What the server can do

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

**ChatGPT:** open [workfinds.app in ChatGPT](https://chatgpt.com/plugins/plugin_asdk_app_6af5a671610c8191aacf3a15581b31ce) and select Install plugin, or search for workfinds in ChatGPT's plugins. If your workspace administrator blocks plugins from the directory, add the server address above as a custom MCP server instead: open Plugins, select the plus button, then Add custom MCP server, name it workfinds, paste the address under Connection and set authentication to none.

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

### Setup files in this repository

| File | For |
|---|---|
| `server.json` | The [MCP registry](https://registry.modelcontextprotocol.io) entry (`app.workfinds/jobs`) |
| `mcp.json`, `plugin.json` | The Cursor plugin: the manifest plus the server entry |
| `gemini-extension.json` | The Gemini CLI extension |
| `llms-install.md` | Setup text for an AI agent that installs the server for you |
| `assets/` | The icon (192, 400 and 512 px PNG) |

## Limits and fair use

Each address may make up to 500 searches and 2,000 job or company lookups a day, and up to 20 searches and 30 lookups a
minute. A search returns at most 50 jobs. Listings change, so confirm details on the employer's site before applying.

## License

MIT, see [LICENSE](LICENSE). It covers the files in this repository, not the workfinds.app service or its name and logo.
