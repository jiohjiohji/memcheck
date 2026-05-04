# Memcheck

Memory health monitor for AI agents. CLI + MCP server.

## Stack
TypeScript, Node.js 20+, Vitest, Commander.js, @modelcontextprotocol/sdk, chalk

## Commands
- `npm run build` — tsc
- `npm test` — vitest run
- `npm run lint` — eslint + prettier --check

## Architecture
- `src/core/` — health scoring (staleness, redundancy, bloat, composite)
- `src/adapters/` — storage plugins (Brain MCP SQLite, Mem0 REST, JSON)
- `src/cli/` — CLI commands (scan, prune, benchmark)
- `src/mcp/` — MCP server (health_check, prune tools)

## Rules
- No `any`. Use `unknown` + type guards.
- All public functions: JSDoc + test.
- TDD: Write failing test FIRST. Then implement. Always.
- Result pattern: `{ ok: true, data } | { ok: false, error }`.
- Adapters: parameterized SQL only. Validate all paths. Never log memory content.
- Concise responses unless asked otherwise.