# AI Skill Library Improvement — Design Spec

Date: 2026-06-25

## Goal

Three simultaneous improvements to ai-skill-library:
1. **Token efficiency** — trim verbose domain review skills to match base/light style
2. **Content quality** — fix overlap, sharpen vague language, add missing edge cases
3. **Missing coverage** — implement the `plain` pack that exists in README but not in the repo

---

## Section 1: Token Efficiency — Skill Trimming

Target style: ~15–18 lines per skill. Base/light skills prove this is sufficient. Domain review skills currently run 38–42 lines, restating knowledge Claude already has.

### Skills to trim

| File | Current lines | Action |
|---|---|---|
| `packs/python/python-review.md` | ~38 | Keep "Fel att flagga" + 5-6 key principles; cut style guide and typing tutorial |
| `packs/python/script-review.md` | ~42 | Keep: exit codes, stderr rule, `__main__` guard, argparse; cut the obvious |
| `packs/backend/db-review.md` | ~40 | Keep: N+1, parametrized queries, table locks, migration reversibility; cut basics |
| `packs/backend/api-review.md` | ~40 | Keep: input validation at boundary, auth check, no stack traces to client; cut HTTP method table |
| `packs/frontend/component-review.md` | ~40 | Keep: missing useEffect deps, key stability, cleanup functions; cut restated hooks rules |

### Skills that stay as-is

All `base/`, all `light/`, all `embedded/`, all `robot/`, all `ci/`, `security/prompt-injection-check.md`, `tdd/tdd.md`.

---

## Section 2: Content Quality

### Fix overlap: `isolation` vs `security-baseline`

Both currently list `~/.ssh`, `~/.aws`, `~/.env` as off-limits.

- `packs/light/isolation.md` — owns the **boundary rule**: what to stay away from and when to ask. Remove the credential path list duplication.
- `packs/base/security-baseline.md` — owns the **audit questions**: what did the agent read/change/run. Remove the file path list, add one-line cross-reference to isolation.

### Sharpen vague language

**`packs/light/session-discipline.md`**
- Replace "Om sessionen driftar: stäng, starta ny session" with a concrete trigger:
  > "Om du gjort mer än ett oplanerat kontextbyte under sessionen: stäng och starta om med ett tydligt mål."

**`packs/base/release-risk-review.md`**
- "Vem ska monitorera och under hur lång tid?" — add default:
  > "Minst under första körningen i produktion."

**`packs/tdd/tdd.md`**
- Add missing common shortcut to the table:
  > "Jag skriver koden först och lägger till tester efteråt" → Tester-efteråt verifierar bara det du vet — inte det du missat

---

## Section 3: Missing Coverage — `plain` pack

### Problem

`plain` is listed in the README as the zero-skills option but `packs/plain/` doesn't exist. Running `ai-skills use plain` currently fails with "Pack 'plain' finns inte."

### Solution

Add `plain` as a special case in `bin/ai-skills`. When `cmd == "use"` and `pack == "plain"`:
- Clear `~/.claude/skills/*.md`
- Write `plain` to `.claude/active-skills.txt`
- Print confirmation: "✓ Pack 'plain' aktiverat — inga skills laddade"
- Do NOT require a pack directory

No `packs/plain/` directory needed. The CLI handles it as a built-in.

---

## Out of scope

- `git` pack — YAGNI, not enough clear use cases yet
- `keybindings`/`config` packs — Claude Code meta, not domain work
- Two-tier (trigger + deep) skill architecture — deferred; Approach A covers the problem sufficiently

---

## Files changed

| File | Change |
|---|---|
| `bin/ai-skills` | Add `plain` special case in `use` branch |
| `packs/python/python-review.md` | Trim to ~15 lines |
| `packs/python/script-review.md` | Trim to ~15 lines |
| `packs/backend/db-review.md` | Trim to ~15 lines |
| `packs/backend/api-review.md` | Trim to ~15 lines |
| `packs/frontend/component-review.md` | Trim to ~15 lines |
| `packs/light/isolation.md` | Remove duplicated credential paths |
| `packs/base/security-baseline.md` | Remove credential paths, add cross-ref to isolation |
| `packs/light/session-discipline.md` | Sharpen drift trigger |
| `packs/base/release-risk-review.md` | Add monitoring default |
| `packs/tdd/tdd.md` | Add missing shortcut row |

11 files total. No new files except the CLI change handling `plain`.
