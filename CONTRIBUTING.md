# Contributing to DogeCode

Such contribute. Much appreciate. Wow.

DogeCode = doge voice layer on top of caveman compression. 30+ agents. Much reach.

Three buckets:

1. **Skill prose** — change how doge speaks, intensity levels, slash commands
2. **New agent** — wire fresh editor/CLI/IDE into unified installer
3. **Hooks/installer** — Claude Code hooks, Node installer, per-repo init

Small focused PR > big rewrite. Doge like simple.

---

## Quick orientation

One skill (`doge`) + sub-skills (`doge-commit`, `doge-review`, `doge-compress`, `cavecrew-*`) distributed to many agents via Claude Code plugin, Codex plugin, Gemini extension, Cursor/Windsurf/Cline rule files, `npx skills`.

Single Node installer at `bin/install.js` detects agents + installs right thing.

Sources of truth = **top level**. Copies under `plugins/caveman/` = **CI-rebuilt**. Don't edit mirrors. Wow.

---

## What to edit

| Want to change... | Edit this |
|---|---|
| Doge behavior (intensity, voice, rules) | `skills/doge/SKILL.md` |
| Commit message format | `skills/doge-commit/SKILL.md` |
| Code review format | `skills/doge-review/SKILL.md` |
| Compress logic | `skills/doge-compress/SKILL.md` + `skills/doge-compress/scripts/` |
| Quick-reference card | `skills/doge-help/SKILL.md` |
| Cavecrew delegation guide | `skills/cavecrew/SKILL.md` |
| Cavecrew subagent definitions | `agents/cavecrew-investigator.md`, `agents/cavecrew-builder.md`, `agents/cavecrew-reviewer.md` |
| Auto-activation rule | `src/rules/caveman-activate.md` |
| Add new agent | `bin/install.js` (PROVIDERS array) |
| Per-repo init script | `src/tools/caveman-init.js` |
| Claude Code hooks | `src/hooks/caveman-*.js`, `src/hooks/caveman-statusline.{sh,ps1}` |
| Settings.json helpers | `bin/lib/settings.js` |
| MCP shrink server | `src/mcp-servers/caveman-shrink/` |

Everything under `plugins/`, `dist/`, or any agent dotdir mirror = build artifact. Edit top-level source only.

---

## What NOT to edit (CI-generated)

CI rebuilds these on every push to `main`. Edits get wiped.

| Path | Source |
|------|--------|
| `plugins/caveman/skills/caveman/SKILL.md` | `skills/doge/SKILL.md` |
| `plugins/caveman/skills/caveman-compress/` | `skills/doge-compress/SKILL.md` + `scripts/` |
| `plugins/caveman/skills/cavecrew/SKILL.md` | `skills/cavecrew/SKILL.md` |
| `plugins/caveman/agents/cavecrew-*.md` | `agents/cavecrew-*.md` |
| `dist/caveman.skill` | ZIP of `skills/doge/` (gitignored) |

---

## Adding a new agent

`bin/install.js` PROVIDERS array = single source of truth.

1. Confirm distribution path — vercel-labs/skills slug OR native plugin/rule-file mechanism
2. Append row to PROVIDERS:
   - `id` — kebab-case (`windsurf`)
   - `label` — display name (`Windsurf`)
   - `mech` — `plugin` / `extension` / `rules-file` / `skills-cli` / …
   - `detect` — clause spec (`command:foo||dir:$HOME/x`)
   - `profile` — vercel-labs/skills slug if applicable
   - `soft: true` — config-dir-only detection (best-effort)
3. `node bin/install.js --list` — confirm row renders. Soft probes show `(soft)`.
4. Add row to `README.md` + `INSTALL.md` install tables.
5. No CI changes needed.

Bad slug = `npx skills add` fails at runtime not load time. Verify against vercel-labs/skills README first. Very important. Wow.

---

## Adding a new skill

1. Create `skills/<name>/SKILL.md`:
   ```yaml
   ---
   name: <name>
   description: <one sentence, present tense>
   ---
   ```
2. Create `skills/<name>/README.md` — human docs, install hint, example.
3. Add `skills/<name>/scripts/` if skill ships helpers.
4. CI sync: add step to `.github/workflows/sync-skill.yml` if it goes in Claude Code plugin.
5. Slash command: add row to `README.md` + `INSTALL.md` slash-command tables.
6. Evals: add prompt to `evals/prompts/en.txt`.

---

## Running tests

```bash
npm test                                          # installer unit + e2e (Node)
python3 -m unittest tests.test_compress_safety    # compress safety (Python)
node tests/test_caveman_init.js                   # per-repo init
node tests/test_symlink_flag.js                   # flag-file symlink safety
```

CI runs all of these on every PR. Tests depending on network/SDK must skip cleanly when deps missing — never gate suite on optional creds.

---

## Running benchmarks + evals

```bash
uv run python benchmarks/run.py     # real Claude API — needs ANTHROPIC_API_KEY in .env.local

python evals/llm_run.py             # regenerate evals/snapshots/results.json
python evals/measure.py             # print token deltas from snapshot
```

Snapshots committed to git. Regenerate only when `SKILL.md` or `evals/prompts/en.txt` changes. Numbers = real runs only. Never invent. Never round. Very serious. Wow.

---

## PR guidelines

- **Conventional Commits** subject — see `skills/doge-commit/SKILL.md`
- **One concern per PR** — README edit and installer fix = separate PRs
- **Update `package.json` `files`** when adding top-level dirs the installer ships to npm
- **Show before/after** for prose changes to any `SKILL.md`
- **Note CI sync** if you edited a source-of-truth file: "CI will resync `plugins/caveman/skills/...` on merge"

PR desc can be short. Doge style fine. Say what changed, why. Done. Wow.

---

## Code style

Such invariants. Many bite before. Keep them.

- **Hooks silent-fail on filesystem errors.** `try/catch` swallowing error = correct. Hook that throws = blocks Claude Code session start = user-facing breakage. See `src/hooks/caveman-activate.js`.
- **Settings.json reads/writes via `bin/lib/settings.js`.** Tolerates JSONC comments. Direct `JSON.parse` crashes on `// comment`. Very bad.
- **Validate hook entries before writing.** Use `validateHookFields()`. Claude Code's Zod schema silently discards **entire** `settings.json` on one bad hook entry. One malformed write = poisoned config. Much oops.
- **Symlink-safe flag writes via `safeWriteFlag()`** in `src/hooks/caveman-config.js`. Predictable path under `$CLAUDE_CONFIG_DIR/`. Without `O_NOFOLLOW` + parent-symlink check = local attacker can clobber any user-writable file.
- **Honor `CLAUDE_CONFIG_DIR`.** Hooks, installer, statusline scripts must respect it. No hardcoded `~/.claude`.
- **`install.sh` + `install.ps1` = 30-line shims.** Delegate to `bin/install.js`. Don't re-add per-OS logic. Quoting bugs live there.

---

## Ideas

See [issues labeled `good first issue`](../../issues?q=label%3A%22good+first+issue%22). Or grep `TODO`/`FIXME` in `src/hooks/`, `bin/`, `src/tools/` — each one = real lead.

U bring doge. Doge put doge in pile. Pile get bigger. Much brain. Such contribute. Wow.
