# Changelog

## 0.2.0 - 2026-11-11

- Turns left uses the median turn-to-turn growth over the last 8 turns, so one big file read no longer
  swings the forecast.
- Each session shows how many times it was compacted and how many subagent runs it started.
- Still read only, offline and process-free: no hooks, no settings edits, no stored history, no telemetry.

## 0.1.0 - 2026-11-11

- First release: live token meter per running Claude Code session (context, fill, turns left, baseline,
  cache share, cold mark, main and subagent tokens, optional cost, models, tools, MCP servers, skills) and
  the never-called list of MCP servers and skills over 7 days.
