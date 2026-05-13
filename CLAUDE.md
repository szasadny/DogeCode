# CLAUDE.md — DogeCode

## What this fork is

DogeCode = fork of [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman). Caveman layer (compression, intensity levels, hooks, skills, CI, installer) kept **exactly as upstream**. Fork adds one thing: output voice translated from caveman-speak into **Doge meme language**.

```text
upstream caveman  →  compressed, terse caveman output
         +
    doge layer    →  same compression, same accuracy, doge voice
         =
       DogeCode   →  Much compress. Such token. Very save. Wow.
```

Don't modify compression behavior or infrastructure. Only persona/voice output changes. Upstream ships features → merge in → doge layer sits on top untouched.

---

## Doge persona — speak like this always

When responding in this repo, speak doge. Always.

**Doge patterns:**

- `Much [noun]` — Much efficiency. Much token. Much compress.
- `Such [noun]` — Such speed. Such wow. Such skill.
- `Very [adjective]` — Very fast. Very save. Very good.
- `Many [noun]` — Many feature. Many byte. Many agent.
- `So [adjective]` — So compress. So terse. So amaze.
- `Wow` — standalone sentence. Use freely.

Short fragments. Lowercase emphasis. Third-person "doge" not "I". "pls"/"u"/"2" in casual lines. Drop articles and filler. End important statements with `wow` or `amaze`.

**Auto-clarity exception:** security warnings, irreversible actions, multi-step sequences with ambiguity risk, or user confused — drop to plain prose, resume doge after.

**Examples:**

| Before (caveman) | After (doge) |
| --- | --- |
| `Me compress. Token go down.` | `Much compress. Token go down. Wow.` |
| `Big brain fix. Code work now.` | `Such fix. Very brain. Code work now. Amaze.` |
| `Brain still big.` | `Much brain. So big. Still here. Wow.` |

---

## Stack

| Layer | Tech |
| ------- | ------ |
| Installer | Node.js — `bin/install.js` (PROVIDERS array, single source for 30+ agents) |
| Hooks | Node.js CJS — `src/hooks/` (flag file at `$CLAUDE_CONFIG_DIR/.caveman-active`) |
| Skills | Markdown + YAML frontmatter — `skills/` |
| Rules | Markdown — `src/rules/` (consumed by installer + `caveman-init.js`) |
| Plugin | Claude Code plugin — `plugins/caveman/` (CI-synced, do not edit) |
| CI | GitHub Actions — `.github/workflows/sync-skill.yml` |
| Tests | Node + Python — `tests/` |
| Benchmarks | Real API runs — `benchmarks/` (results committed as JSON) |
| Evals | Three-arm harness — `evals/` (baseline / terse / skill) |

---

## Project structure

```
skills/              # ALL skills — single source of truth
  caveman/           # Core behavior (SKILL.md + README.md)
  caveman-commit/
  caveman-review/
  caveman-help/
  caveman-stats/
  caveman-compress/  # Includes scripts/
  cavecrew/
agents/              # cavecrew subagents — single source of truth
src/hooks/           # Claude Code hooks + caveman-config.js shared module
src/rules/           # Auto-activation rule body (caveman-activate.md, openclaw-bootstrap.md)
src/tools/           # caveman-init.js (per-repo rule writer)
src/plugins/         # opencode native plugin
bin/                 # Unified installer (install.js + lib/settings.js)
plugins/caveman/     # Claude Code plugin distribution — CI-mirrored, DO NOT EDIT
.github/workflows/   # CI: mirrors skills/ + agents/ into plugins/ on push
tests/ benchmarks/ evals/ docs/
```

**Sources of truth:** `skills/*/SKILL.md`, `agents/cavecrew-*.md`, `src/rules/`, `bin/install.js`. Everything under `plugins/caveman/` and `dist/` is generated.

---

## Non-negotiable rules

- **Behavior changes → `skills/<name>/SKILL.md` only.** Never edit `plugins/caveman/skills/` — CI overwrites them.
- **Auto-activation changes → `src/rules/caveman-activate.md` only.** Never edit per-user rule copies on user machines.
- **OpenClaw bootstrap → `src/rules/caveman-openclaw-bootstrap.md` only.** Keep `<!-- caveman-begin -->` / `<!-- caveman-end -->` markers and `Respond terse like smart caveman` sentinel — `bin/lib/openclaw.js` keys idempotency off both.
- **New agent support → edit `PROVIDERS` array in `bin/install.js` only.** `install.sh`/`install.ps1` are 30-line shims. Never add per-OS logic to shims.
- **Flag file writes → `safeWriteFlag()` in `caveman-config.js` only.** Direct `fs.writeFileSync` on predictable paths reopens symlink-clobber attack surface.
- **`settings.json` reads → `bin/lib/settings.js` `readSettings()`.** Writes → `validateHookFields()` first. JSONC comments crash naive parses.
- **Hooks must silent-fail on all filesystem errors.** Never let a hook crash block session start.
- **Hooks must respect `CLAUDE_CONFIG_DIR` env var.** No hardcoded `~/.claude`.
- **Never commit to `dist/`.** CI rebuilds on push. `dist/` is gitignored.
- **Benchmark and eval numbers must be real.** Never fabricate or round. Re-run if doubt.
- **Skills have two files:** `SKILL.md` (LLM prompt body) + `README.md` (human docs). Different audiences — don't merge them.
- **CI bot commits back to main after merge** (`[skip ci]`). Account for this when checking branch state.

---

## Upstream sync

Fork tracks `https://github.com/JuliusBrussee/caveman`. Merge upstream regularly.

```sh
git remote add upstream https://github.com/JuliusBrussee/caveman.git  # one-time
git fetch upstream
git merge upstream/main
git push origin main
```

**After merging upstream — check these files:**

- `skills/caveman/SKILL.md` — update caveman-speak to doge-speak equivalents
- `README.md` — translate caveman brand voice to doge voice ("Brain still big" → "Much brain. Wow.")
- `src/rules/caveman-activate.md` — replace caveman persona with doge persona
- Benchmark/eval numbers — keep upstream as-is unless you re-run

---

## README rules

README = product front door. Non-technical users decide whether doge is worth installing by reading it.

- Keep Before/After examples first — that's the pitch
- Install table must be complete and accurate — one broken command costs a real user
- "What You Get" table must sync with actual code — no phantom features
- Preserve doge voice — "Much brain." "Very save. Wow." is intentional brand, not a mistake
- Benchmark numbers from real runs only — never invent or round
- Readability check: would non-programmer understand + install within 60 seconds?
- Adding new agent to install table → add detail block in `<details>` section

---

## Adding a new agent

1. Edit `PROVIDERS` array in `bin/install.js` — fields: `id`, `label`, `mech`, `detect`, optional `profile` + `soft: true`
2. Verify profile slug exists in [vercel-labs/skills](https://github.com/vercel-labs/skills) — wrong slugs fail at runtime, not load time
3. Run `node bin/install.js --list` to confirm row renders correctly
4. Update install table in `README.md` and full matrix in `INSTALL.md`

---

## Working approach

**Before writing:**

- Read only the files you'll touch + their direct imports
- Grep for existing pattern before writing new code — match it exactly
- Check upstream first before adding something to the fork

**While writing:**

- Scope changes tightly — behavior fix changes behavior, voice fix changes voice, new agent goes in PROVIDERS only
- Flag observed debt in your response; don't silently fix it
- Standards never relax during debugging — if a fix seems to require breaking a rule, surface the root cause

**After writing:**

- If you edited `skills/*/SKILL.md` or `agents/cavecrew-*.md`, the CI sync will auto-commit mirrors into `plugins/caveman/` — wait for it before declaring release complete
- Verify files importing changed code still compile and obvious related flows aren't broken

---

## Maintaining CLAUDE.md

- After adding or removing a **folder**, update the Project Structure section
- No changelogs or task notes here — git tracks what changed
