Run quality gate. All must pass before committing.

1. `npm run build` — zero errors
2. `npm test` — all pass
3. `npm run lint` — zero warnings
4. Use security-auditor subagent on files changed since last commit (`git diff --name-only HEAD`)

Report: ✅/❌ for each. If ANY fails, list specifics and suggest fixes.