# Storage Adapters

## When to use
When working on files in `src/adapters/`.

## Adapter Interface
Every adapter must implement:
- connect(config) → Promise<void>
- getEntries(options?) → Promise<MemoryEntry[]>
- getStats() → Promise<StoreStats>
- deleteEntries(ids: string[]) → Promise<number>
- close() → Promise<void>

## Brain MCP (SQLite) — Priority 1
- User provides path to .db file
- Tables: memories (id, content, embedding, created_at, last_accessed, metadata)
- Timestamps are ISO 8601 strings (like "2026-05-04T10:30:00Z"), NOT Unix numbers
- Read-only by default. Write operations need --write flag.

## Security Rules (Critical)
- NEVER log memory content — only IDs and scores
- Validate all file paths: resolve the path, then check it doesn't escape the expected directory
- SQLite: use parameterized queries ONLY — never put variables directly in SQL strings
- Example of WRONG: `SELECT * FROM memories WHERE id = '${id}'` ← SQL injection risk
- Example of RIGHT: `db.prepare('SELECT * FROM memories WHERE id = ?').get(id)` ← safe