# Token Meter (directory edition)

See what each running Claude Code session is spending: context size, window fill, baseline, cache share, a
cold-cache mark, subagent tokens, compactions, and calls per tool, MCP server and skill. It also shows what each
CLAUDE.md, rule, MEMORY.md and skill header costs per call, lists personal skills you never call, and proposes
what to cut. Read only, offline, numbers and names only, never prompt text.

This folder is the **directory edition**: Markdown only. It ships no scripts. The skill does its work with Claude
Code's built-in tools: short `find`, `grep` and `awk` commands over the `usage` fields in
`~/.claude/projects/**/*.jsonl`. No network calls, no telemetry, and it never writes a log or setting.

## Full edition

The full edition lives at the repository root: <https://github.com/maumoya/token-meter>. It has the
`token_meter.py` script, tests, evals and benchmarks.

### Full edition only

- The "turns left before compaction" forecast.
- The status line meter (`--statusline`).
- Costs in money from a price file (`--prices`), and the `--max-fill` budget gate for scripts and CI.
- The list of configured MCP servers you never call (it reads `~/.claude.json`, which this edition leaves alone).
- JSON output and the GitHub Action.

## Install

From the plugin directory, install **token-meter**. The repository also has its own marketplace:

```
/plugin marketplace add maumoya/token-meter
/plugin install token-meter@token-meter
```

That marketplace entry installs the full edition from the repository root.

## Use

Say "token meter", "how full is my context" or "what should I cut". See
[skills/token-meter/SKILL.md](skills/token-meter/SKILL.md).

## License

MIT. See [LICENSE](LICENSE).
