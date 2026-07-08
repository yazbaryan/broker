# broker — scheduled trading routine

A minimal repo whose only job is to run the **Broker** trading strategy as a
Claude Code **cloud routine** on a weekday schedule. It contains no app code; the
routine reaches the deployed Broker server purely over remote MCP/HTTPS.

## What's here

| File | Purpose |
|------|---------|
| `.mcp.json` | Connects the remote `broker` MCP server; auth from `${BROKER_API_TOKEN}` |
| `.claude/commands/run-strategy.md` | The full run procedure the routine follows |
| `CLAUDE.md` | Context loaded on every run |
| `.gitignore` | Guards against committing secrets |

**No secrets live in this repo.** The bearer token is provided at run time via the
`BROKER_API_TOKEN` environment variable.

## One-time cloud-routine setup (in claude.ai/code)

1. **Connect this GitHub repo** to Claude Code (authorize the GitHub app for
   `yazbaryan/broker`).
2. **Environment variable:** set `BROKER_API_TOKEN=<your token>` on the routine's
   cloud environment. (Note: routine env vars are visible to anyone who can edit
   the environment — there is no encrypted vault yet.)
3. **Allowed network domains:** ensure `broker.yazbaryan.am` is reachable from the
   environment.
4. **Schedule:** cron `0 17 * * 1-5` (weekdays 17:00; adjust for the routine's
   timezone). Prompt: *"Run /run-strategy — execute the Broker trading strategy
   run."*

## Running locally instead

With `BROKER_API_TOKEN` exported in your shell, open this repo in Claude Code and
run `/run-strategy`.
