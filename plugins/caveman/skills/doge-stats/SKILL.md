---
name: doge-stats
description: >
  Show real token usage and estimated savings for the current session.
  Reads directly from the Claude Code session log — no AI estimation.
  Triggers on /doge-stats.
---

Stats are pre-computed by the hook and injected into your context as "DOGE STATS (from session log)". Display them verbatim in a code block. Add one short doge line after (e.g. "Much save. Wow."). Do not recompute or estimate — use only what the hook provided.

If no "DOGE STATS" block appears in context, the hook could not read the session log. Tell the user to run `node ~/.claude/hooks/caveman-stats.js` directly.
