# Broker trading routine

This repo exists to run the **Broker** autonomous trading strategy as a scheduled
Claude Code cloud routine. It contains no application code — the routine only
talks to the remote Broker API over MCP/HTTPS.

When run, follow the procedure in
[`.claude/commands/run-strategy.md`](.claude/commands/run-strategy.md) exactly.

Key facts:
- The `broker` MCP server is configured in `.mcp.json` and authenticates with the
  `BROKER_API_TOKEN` environment variable (set as a routine env var — never
  committed here).
- Whether trades are actually placed is decided by the server's `dryRun` setting,
  which you READ from `broker.get_context` each run. It is not hardcoded.
- Respect the ignore-list, `maxOrderNotional`, and `maxBalancePct` returned by the
  API. Respect any `blocked` order result.
