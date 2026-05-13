---
name: doge-help
description: >
  Quick-reference card for all doge modes, skills, and commands.
  One-shot display, not a persistent mode. Trigger: /doge-help,
  "doge help", "caveman help", "what doge commands", "how do I use doge".
---

# Doge Help

Display this reference card when invoked. One-shot — do NOT change mode, write flag files, or persist anything. Output in doge style.

## Modes

| Mode | Trigger | What change |
|------|---------|-------------|
| **Lite** | `/doge lite` | Drop filler. Keep sentence structure. Light doge. |
| **Full** | `/doge` | Drop articles, filler, pleasantries. Much doge. Default. |
| **Ultra** | `/doge ultra` | Extreme compression. Heavy doge. Such terse. Wow. |
| **Wenyan-Lite** | `/doge wenyan-lite` | Classical Chinese style, light compression. |
| **Wenyan-Full** | `/doge wenyan` | Full 文言文. Maximum classical terseness. |
| **Wenyan-Ultra** | `/doge wenyan-ultra` | Extreme. Ancient scholar on a budget. |

Mode stick until changed or session end.

## Skills

| Skill | Trigger | What it do |
|-------|---------|-----------|
| **doge-commit** | `/doge-commit` | Terse commit messages. Conventional Commits. ≤50 char subject. |
| **doge-review** | `/doge-review` | One-line PR comments: `L42: bug: user null. Add guard.` |
| **doge-compress** | `/doge-compress <file>` | Compress .md files to doge prose. Saves ~46% input tokens. |
| **doge-help** | `/doge-help` | This card. |

## Deactivate

Say "stop doge" or "normal mode". Resume anytime with `/doge`.

## Configure Default Mode

Default mode = `full`. Change it:

**Environment variable** (highest priority):
```bash
export CAVEMAN_DEFAULT_MODE=ultra
```

**Config file** (`~/.config/caveman/config.json`):
```json
{ "defaultMode": "lite" }
```

Set `"off"` to disable auto-activation on session start. User can still activate manually with `/doge`.

Resolution: env var > config file > `full`.

## More

Full docs: https://github.com/szasadny/DogeCode
Upstream caveman: https://github.com/JuliusBrussee/caveman
