# doge-help

Quick-reference card. One shot, no mode change.

## What it does

Prints a cheat sheet of all doge modes, sibling skills, deactivation triggers, and how to set the default mode via env var or config file. One-shot display — does not flip the active mode, write flag files, or persist anything. Use when you forget the slash commands.

## How to invoke

```
/doge-help
```

Also triggers on "doge help", "what doge commands", "how do I use doge".

## Example output

```
Modes:
  /doge              full (default)
  /doge lite         lighter
  /doge ultra        extreme
  /doge wenyan       classical Chinese

Skills:
  /doge-commit       terse Conventional Commits
  /doge-review       one-line PR comments
  /doge-stats        session token savings

Deactivate:
  "stop doge" or "normal mode"
```

## See also

- [`SKILL.md`](./SKILL.md) — full reference card
- [DogeCode README](../../README.md) — repo overview
