# Install the workfinds MCP server

workfinds is a remote MCP server: there is nothing to download or run. Add it by address.

- Server name: `workfinds`
- Transport: Streamable HTTP
- Address: `https://workfinds.app/mcp`
- Authentication: none (no API key, no sign-in)

Add this to the client's MCP settings:

```json
{
  "mcpServers": {
    "workfinds": {
      "url": "https://workfinds.app/mcp"
    }
  }
}
```

If the client needs the transport named, use `streamable-http` (or `http`). Then run one `search_jobs` call, for example
`{"query": "data engineer", "country": "PH", "work_arrangement": ["remote"]}`, to check that it answers.
