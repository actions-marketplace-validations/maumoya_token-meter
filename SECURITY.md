# Security policy

## Reporting a vulnerability

If you find a way to make the meter print prompt text, a file path or a secret, or to make it write,
delete or send anything, report it privately through GitHub's
[private vulnerability reporting](https://github.com/maumoya/token-meter/security/advisories/new).
You will get an answer within 7 days.

## What the tool does and does not do

- It reads the Claude Code session logs under `~/.claude/projects`, `~/.claude/settings.json` (only the
  auto-compact window), `~/.claude.json` (only the MCP server names, never their values) and the folder
  names under `~/.claude/skills`. All reads are read only.
- It prints numbers, model ids, short session ids and tool, MCP server and skill names. A name that is not
  a plain identifier prints as `other`. Any output string over 80 characters stops the run.
- It writes no file, opens no network connection, starts no process, installs no hook and edits no setting.
  The tests check the source for network and process imports and for file writes.
- It has no dependencies beyond the Python standard library.

## Supported versions

Only the latest version on `main` is supported.
