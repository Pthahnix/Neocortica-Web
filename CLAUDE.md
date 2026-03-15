# neocortica-web

Lightweight MCP server for web page fetching and caching via Apify rag-web-browser.

## Architecture

2 tools: `web_fetching` (URL → Apify REST API → markdown → cache) and `web_content` (read cached markdown).

## Development

- Node.js ESM, TypeScript, `@modelcontextprotocol/sdk`
- Tests: Node.js built-in `test` module, files in `.test/` mirroring `src/`
- Test artifact prefix: `zztest_`, cleanup in `afterEach`
- Gate rule: ALL tests must pass before next component

## Commands

```bash
npm run mcp    # Start MCP server
npm test       # Run all tests
npm run build  # TypeScript compile
```

## Environment

- `APIFY_TOKEN` — Apify API authentication (required)
- `NEOCORTICA_CACHE` — Cache directory (default: `.cache`)
