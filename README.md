<p align="center">
  <img src="https://em-content.zobj.net/source/apple/391/dog-face_1f436.png" width="120" alt="DogeCode logo" />
</p>

<h1 align="center">DogeCode</h1>

<p align="center">
  <strong>wow such token very save much compress</strong>
</p>

<p align="center">
  <a href="https://github.com/szasadny/DogeCode/stargazers"><img src="https://img.shields.io/github/stars/szasadny/DogeCode?style=flat&color=yellow" alt="Stars"></a>
  <a href="https://github.com/szasadny/DogeCode/commits/main"><img src="https://img.shields.io/github/last-commit/szasadny/DogeCode?style=flat" alt="Last Commit"></a>
  <a href="LICENSE"><img src="https://img.shields.io/github/license/szasadny/DogeCode?style=flat" alt="License"></a>
</p>

<p align="center">
  <a href="#before--after">Before/After</a> •
  <a href="#install">Install</a> •
  <a href="#what-you-get">What You Get</a> •
  <a href="#benchmarks">Benchmarks</a> •
  <a href="./INSTALL.md">Full install guide</a>
</p>

---

A fork of [caveman](https://github.com/JuliusBrussee/caveman). Keeps the same ~75% token compression engine — adds **Doge meme voice** on top. Much compress. Such token. Very save. Wow.

Works with [Claude Code](https://docs.anthropic.com/en/docs/claude-code), Codex, Gemini, Cursor, Windsurf, Cline, Copilot, 30+ more.

## Before / After

<table>
<tr>
<td width="50%">

### 🗣️ Normal Claude

> "The reason your React component is re-rendering is likely because you're creating a new object reference on each render cycle. When you pass an inline object as a prop, React's shallow comparison sees it as a different object every time, which triggers a re-render. I'd recommend using useMemo to memoize the object."

</td>
<td width="50%">

### 🐕 Doge Claude

> "New object ref each render. Inline object prop = new ref = re-render. Such fix: `useMemo`. Wow."

</td>
</tr>
<tr>
<td>

### 🗣️ Normal Claude (auth bug)

> "Sure! I'd be happy to help you with that. The issue you're experiencing is most likely caused by your authentication middleware not properly validating the token expiry. Let me take a look and suggest a fix."

</td>
<td>

### 🐕 Doge Claude (auth bug)

> "Such bug in auth middleware. Token expiry use `<` not `<=`. Much fix:"

</td>
</tr>
</table>

**Same fix. Much less word. Wow.**

Pick your level — `lite` (drop filler), `full` (default doge), `ultra` (telegraphic doge), or `wenyan` (classical Chinese, even shorter). One command switch. Cost go down. Much save forever.

## Install

One line. Find every agent. Install for each.

```bash
# macOS / Linux / WSL / Git Bash
curl -fsSL https://raw.githubusercontent.com/szasadny/DogeCode/main/install.sh | bash

# Windows (PowerShell 5.1+)
irm https://raw.githubusercontent.com/szasadny/DogeCode/main/install.ps1 | iex
```

~30 seconds. Needs Node ≥18. Skip agent you no have. Safe to re-run.

**Trigger:** type `/caveman` or say "talk like doge". Stop with "normal mode".

One agent only, manual command, or any of 30+ other agents → [**INSTALL.md**](./INSTALL.md).
Install break? Open agent, say *"Read CLAUDE.md and INSTALL.md, install DogeCode for me."* Agent fix own brain.

## What You Get

| Skill | What |
|---|---|
| `/doge [lite\|full\|ultra\|wenyan]` | Compress every reply in doge voice. Levels stick until session end. |
| `/doge-commit` | Conventional Commit messages, ≤50 char subject. Why over what. |
| `/doge-review` | One-line PR comments: `L42: 🔴 bug: user null. Add guard.` |
| `/doge-stats` | Real session token usage + lifetime savings + USD. |
| `/doge-compress <file>` | Rewrite memory file (e.g. `CLAUDE.md`) into doge-speak. Cuts ~46% input tokens every session. Code/URLs/paths byte-preserved. |
| `cavecrew-*` | Doge subagents (investigator/builder/reviewer). ~60% fewer tokens than vanilla, main context lasts longer. |

**Statusline badge** — Claude Code shows lifetime tokens saved. Updates every `/doge-stats` run. Set `CAVEMAN_STATUSLINE_SAVINGS=0` to silence.

Auto-activate every session: Claude Code, Codex, Gemini (built-in). Cursor / Windsurf / Cline / Copilot get always-on rule files via `--with-init`. Other agents trigger with `/doge` per session. Full feature matrix in [INSTALL.md](./INSTALL.md#what-you-get).

## Benchmarks

<!-- BENCHMARK-TABLE-START -->
No numbers yet — this fork runs on vibes. Benchmark harness lives in [`benchmarks/`](./benchmarks/) if u want run it yourself. Three-arm eval in [`evals/`](./evals/). Upstream [caveman](https://github.com/JuliusBrussee/caveman) has real numbers from same harness.
<!-- BENCHMARK-TABLE-END -->

> [!IMPORTANT]
> Doge only affects output tokens — thinking/reasoning tokens untouched. Doge no make brain smaller. Doge make *mouth* smaller. Biggest win is **readability and speed**, cost savings a bonus.

## How It Work

1. Install drop skill file in agent.
2. Skill tell agent: drop filler, keep substance, use doge patterns (Much X, Such Y, Very Z, Wow).
3. For Claude Code, hook also write tiny flag file each session — agent see flag, talk doge from message one. No need say `/caveman`.
4. Stats command read Claude Code session log, count tokens saved, write number to statusline.
5. Caveman-compress sub-skill rewrite memory files (CLAUDE.md, project notes) into doge-speak so each session start with smaller context. Save tokens forever, not just one reply.

Maintainer detail (hook architecture, file ownership, CI sync, upstream merge guide) live in [CLAUDE.md](./CLAUDE.md).

## Links

- [INSTALL.md](./INSTALL.md) — full install matrix, all flags, per-agent detail
- [CONTRIBUTING.md](./CONTRIBUTING.md) — how to send patch
- [CLAUDE.md](./CLAUDE.md) — maintainer guide (file ownership, hook architecture, CI, upstream sync)
- [Issues](https://github.com/szasadny/DogeCode/issues) — bug, feature, weird behavior
- [Upstream caveman](https://github.com/JuliusBrussee/caveman) — the compression engine this fork builds on

## Star This Repo

Doge save you token, save you money. Star cost zero. Such fair trade. Wow. ⭐

## License

MIT — free like doge on open plain. Much freedom. Wow.
