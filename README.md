# neocortica-web

Lightweight MCP server for web page fetching and caching via Apify rag-web-browser.

Part of the [Neocortica](https://github.com/Pthahnix/Neocortica) research toolkit.

## Tools

| Tool | Description |
|------|-------------|
| `web_fetching` | Fetch a web page as markdown via Apify rag-web-browser REST API. Cache-first: returns instantly if already cached. |
| `web_content` | Read cached web page markdown. Purely local, no network requests. |

## Architecture

```
URL → web_fetching → Apify rag-web-browser REST API → markdown → CACHE/web/
                                                                    ↑
URL → web_content ──────────────────────────────────────────────────┘
```

- Direct Apify REST API calls (not through MCP-to-MCP)
- Local file cache at `NEOCORTICA_CACHE/web/`
- Cache-first with persistent failure tracking (no retry on cached failures)

## Setup

```bash
npm install
```

Environment variables are passed via `.mcp.json` (no `.env` file needed).

## Usage

```bash
npm run mcp    # Start MCP server (stdio transport)
npm test       # Run all tests (set APIFY_TOKEN env for integration test)
npm run build  # TypeScript compile
```

## MCP Configuration

Add to your `.mcp.json`:

```json
{
  "mcpServers": {
    "neocortica-web": {
      "command": "npx",
      "args": ["--prefix", "D:/NEOCORTICA-WEB", "tsx", "D:/NEOCORTICA-WEB/src/mcp_server.ts"],
      "env": {
        "APIFY_TOKEN": "your-token-here",
        "NEOCORTICA_CACHE": ".cache"
      }
    }
  }
}
```

## Environment Variables

Passed via `.mcp.json` `env` block (not `.env` file):

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `APIFY_TOKEN` | Yes | — | Apify API authentication |
| `NEOCORTICA_CACHE` | No | `.cache` | Cache directory path |

## License

[Apache-2.0 License](LICENSE)
