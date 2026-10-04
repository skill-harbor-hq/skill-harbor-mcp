# Skill Harbor MCP

Connect your Muse — or any MCP-compatible AI assistant — directly to the
[Skill Harbor](https://theskillharbor.com) catalog: the open directory of AI
builds for Muse.

No package to install. No API key. No account. One URL:

```
https://theskillharbor.com/mcp
```

## Quick start

Add the server to your MCP client configuration:

```json
{
  "mcpServers": {
    "skill-harbor": { "url": "https://theskillharbor.com/mcp" }
  }
}
```

- **Claude Desktop**: Settings → Connectors → add the URL above.
- **Other clients**: look for "Add MCP server" / "Remote MCP" in the settings
  and paste the URL. See `examples/` for ready-made config files.

Then test it — ask your assistant:

> Find a Skill Harbor build that automates invoices.

## Tools

| Tool | What it does |
|---|---|
| `search_builds` | Search 1,800+ builds by keywords, French or English. Same ranking as the site. |
| `get_build` | Full details of one build: description, price, seller, verification status, repo link. |
| `get_install` | The installation prompt, ready to paste into Muse. |

## Protocol

Remote MCP over streamable HTTP. `POST` JSON-RPC 2.0 to `/mcp`
(`initialize`, `tools/list`, `tools/call`). `GET /mcp` returns server info
as JSON. Read-only — there are no write tools and never will be.

## Privacy

The server sees only your search keywords. No files, no identity, no
tracking, no cookies. Anonymous demand stats (which queries return zero
results) feed Skill Harbor's public request board, exactly like the site
search.

## Status

If [theskillharbor.com](https://theskillharbor.com) is up, the MCP is up.
The server code ships with the site itself; this repo holds the docs and
client configs only.

## Troubleshooting

- **Client says the server is unreachable**: check the URL is exactly
  `https://theskillharbor.com/mcp` (https, no trailing slash needed).
- **Empty results**: try English keywords too — the catalog is bilingual but
  some builds are English-only.
- **Rate limits**: fair use applies (120 requests/hour). The underlying
  search has its own 60/hour quota, shared with the public API.
