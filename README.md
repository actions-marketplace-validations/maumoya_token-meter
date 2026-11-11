# claude-token-meter

[![Tests](https://github.com/maumoya/claude-token-meter/actions/workflows/test.yml/badge.svg)](https://github.com/maumoya/claude-token-meter/actions/workflows/test.yml)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

**Live token meter for Claude Code.** See what every running session is spending right now: context size,
how full the auto-compact window is, turns left before compaction, cache share, a cold-cache warning,
main versus subagent tokens, and the MCP servers and skills you never call.

Every Claude Code call re-reads the whole context, so context size is the cost driver. This meter makes it
visible, per session, so you know when to compact, when to start fresh and what to switch off.

```
3 live session(s) in the last 15 min · auto-compact window 200k (settings env)
  3e359cce  ctx  166k  83% · turns left   - · cache 93% · base 113k · spent 37.4M (sub 347k) · no price · claude-opus-5-5
      tools Bash 221, Write 22, Edit 12, Read 9 · MCP github 34 · skills code-review 2
  16439f1d  ctx  161k  81% · turns left  20 · cache 97% COLD · base 91k · spent 55.8M (sub 152k) · no price · claude-opus-5-5
      tools Bash 327, Write 17, Read 12
  never called in 7 days, MCP servers: notion
  never called in 7 days, skills: old-skill, unused-skill
```

## Install

As a Claude Code plugin:

```
/plugin marketplace add maumoya/claude-token-meter
/plugin install claude-token-meter@claude-token-meter
```

Then ask Claude "how full is my context?" or run `/claude-token-meter`.

Or run the script directly (Python 3.9+, nothing to install):

```bash
python3 skills/claude-token-meter/scripts/token_meter.py --unused
```

## What it shows

| Field | Meaning |
|---|---|
| `ctx` / `%` | context of the latest call, and how full the auto-compact window is |
| `turns left` | turns until compaction at the recent growth rate |
| `base` | context of the first call: your fixed cost (instructions, MCP tool lists, skills) |
| `cache` | share of input read from the prompt cache |
| `COLD` | idle past the cache life (5 min, or 1 h for the long cache): the next call re-writes it all |
| `spent` / `sub` | all tokens of the session, and the part used by subagents |
| tools, MCP, skills | calls per tool, MCP server and skill |
| never called | connected MCP servers and personal skills no session used in 7 days (`--unused`) |

Options: `--minutes N` (live window, default 15), `--window N` (context window, default from
`~/.claude/settings.json`, else 200000), `--prices FILE` (cost; see `examples/prices.example.json`),
`--json`, `--root DIR`.

Cost is shown only when you pass a price file. The meter never guesses prices.

## Privacy and safety

- **Read only and offline.** It reads `~/.claude/projects/**/*.jsonl`, the auto-compact window from
  `~/.claude/settings.json`, the MCP server names (never their values) from `~/.claude.json` and the folder
  names under `~/.claude/skills`. It writes nothing, opens no network connection and starts no process.
- **Numbers and names only.** No prompt, reply, file path or file content ever reaches the output. A name
  that is not a plain identifier prints as `other`, and any output string over 80 characters stops the run.
- **No dependencies.** Python standard library only. The tests check that the source imports nothing that
  talks to the network or runs programs, and never opens a file for writing.

See [SECURITY.md](SECURITY.md).

## Tests

```bash
python3 -m unittest discover -s tests -v
```

## License

MIT, see [LICENSE](LICENSE). Made by Mauricio Alonso Moya Tapia ([@maumoya](https://github.com/maumoya)).
