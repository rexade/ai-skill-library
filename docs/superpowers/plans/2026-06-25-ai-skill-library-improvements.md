# AI Skill Library Improvements — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Trim verbose domain skills to ~15 lines, fix two overlapping skills, sharpen three skills with vague language, and add `plain` as a working CLI option.

**Architecture:** Pure file edits — 10 markdown files and 1 bash script. No new files. Tasks are fully independent; any order works. Each task ends with a commit.

**Tech Stack:** Bash (CLI), Markdown (skill files)

## Global Constraints

- Target line count per trimmed skill: 15–18 lines (including frontmatter)
- Language: Swedish throughout all skill files
- Do not change frontmatter `name:` or `description:` fields unless specified
- Skills that are NOT in scope: all of `base/`, all of `light/`, all of `embedded/`, all of `robot/`, all of `ci/`, `security/prompt-injection-check.md`, `tdd/tdd.md` (except the one-row addition in Task 3)

---

### Task 1: Add `plain` pack support to CLI

**Files:**
- Modify: `bin/ai-skills`

**Interfaces:**
- Produces: `ai-skills use plain` clears skills and writes `plain` to `.claude/active-skills.txt`; `ai-skills list` includes `plain` in output

- [ ] **Step 1: Add `plain` special case in the `use` branch**

In `bin/ai-skills`, find the block after the wrong-directory check and before `pack_path="$PACKS_DIR/$pack"`. Insert:

```bash
    if [[ "$pack" == "plain" ]]; then
      skills_dir=".claude/skills"
      mkdir -p "$skills_dir"
      rm -f "$skills_dir"/*.md
      echo "plain" > .claude/active-skills.txt
      if [[ -d .git ]]; then
        gitignore=".gitignore"
        touch "$gitignore"
        grep -qxF ".claude/skills/" "$gitignore" || echo ".claude/skills/" >> "$gitignore"
        grep -qxF ".claude/active-skills.txt" "$gitignore" || echo ".claude/active-skills.txt" >> "$gitignore"
      fi
      echo "✓ Pack 'plain' aktiverat — inga skills laddade"
      exit 0
    fi
```

- [ ] **Step 2: Update `list` to include `plain`**

Find the `list)` branch:
```bash
  list)
    echo "Tillgängliga packs:"
    ls "$PACKS_DIR/" | sed 's/^/  - /'
    ;;
```

Replace with:
```bash
  list)
    echo "Tillgängliga packs:"
    echo "  - plain"
    ls "$PACKS_DIR/" | sed 's/^/  - /'
    ;;
```

- [ ] **Step 3: Verify `plain` works**

From any directory that is NOT `~/ai-skill-library`:
```bash
cd ~ && ai-skills use plain
```
Expected output:
```
✓ Pack 'plain' aktiverat — inga skills laddade
```

```bash
ai-skills status
```
Expected output:
```
Aktivt pack: plain
Skills:
```
(No skills listed — that's correct.)

```bash
ai-skills list
```
Expected: `plain` appears first in the list.

- [ ] **Step 4: Commit**

```bash
cd ~/ai-skill-library
git add bin/ai-skills
git commit -m "feat: lägg till plain som inbyggt pack i CLI"
```

---

### Task 2: Fix overlap between `isolation` and `security-baseline`

**Files:**
- Modify: `packs/base/security-baseline.md`

**Context:** `isolation.md` owns the boundary rule (what to stay away from, file paths). `security-baseline.md` owns audit questions (what did the agent do?). Both currently list `~/.ssh`, `~/.env`, `~/.aws`. Remove the paths from `security-baseline` and add a cross-reference to `isolation`.

- [ ] **Step 1: Rewrite `security-baseline.md`**

Replace the entire file content with:

```markdown
---
name: security-baseline
description: Use when an agent has shell access, file access, or calls external APIs — checks for injection and privilege risks
---

# Security Baseline

Ställ dessa frågor vid varje agentkörning:

## Prompt Injection
- Läste agenten opålitligt innehåll? (PR-kommentarer, README, PDFs, e-post)
- Kunde fientlig input ha styrt agentens beteende?

## Filåtkomst
- Nådde agenten bara projektmappen? (Se isolation-skillen för filgränser)

## Behörigheter
- Körde agenten med minsta nödvändiga behörighet?
- Kördes deployer eller farliga kommandon utan explicit instruktion?

## Bevis
- Vad läste agenten?
- Vad ändrade agenten?
- Vilket kommando körde agenten?

**Låt aldrig bekvämlighet springa ifrån isolering.**
```

- [ ] **Step 2: Verify**

```bash
wc -l ~/ai-skill-library/packs/base/security-baseline.md
```
Expected: ≤ 22 lines.

```bash
grep -c "ssh\|aws\|env" ~/ai-skill-library/packs/base/security-baseline.md
```
Expected: `0` (paths removed).

- [ ] **Step 3: Commit**

```bash
cd ~/ai-skill-library
git add packs/base/security-baseline.md
git commit -m "refactor: ta bort duplicerade filsökvägar från security-baseline, hänvisa till isolation"
```

---

### Task 3: Sharpen vague language in three skills

**Files:**
- Modify: `packs/light/session-discipline.md`
- Modify: `packs/base/release-risk-review.md`
- Modify: `packs/tdd/tdd.md`

- [ ] **Step 1: Sharpen `session-discipline.md` drift trigger**

In `packs/light/session-discipline.md`, find:
```
- Om sessionen driftar: stäng, starta ny session med ett tydligt mål
```

Replace with:
```
- Om du gjort mer än ett oplanerat kontextbyte under sessionen: stäng och starta om med ett tydligt mål
```

- [ ] **Step 2: Add monitoring default to `release-risk-review.md`**

In `packs/base/release-risk-review.md`, find:
```
- Vem ska monitorera och under hur lång tid?
```

Replace with:
```
- Vem ska monitorera och under hur lång tid? (Minst under första körningen i produktion)
```

- [ ] **Step 3: Add missing shortcut row to `tdd.md`**

In `packs/tdd/tdd.md`, find the table:
```
| "Det är för enkelt för ett test" | Enkla saker har buggar också |
| "Jag testar efteråt" | Tester-efteråt verifierar bara det du vet — inte det du missat |
| "Jag vet hur det ska fungera" | Vetande ≠ bevis |
```

Replace with:
```
| "Det är för enkelt för ett test" | Enkla saker har buggar också |
| "Jag testar efteråt" | Tester-efteråt verifierar bara det du vet — inte det du missat |
| "Jag vet hur det ska fungera" | Vetande ≠ bevis |
| "Jag skriver koden först och lägger till tester efteråt" | Tester-efteråt verifierar bara det du vet — inte det du missat |
```

- [ ] **Step 4: Verify all three files look correct**

```bash
grep "oplanerat kontextbyte" ~/ai-skill-library/packs/light/session-discipline.md
grep "första körningen" ~/ai-skill-library/packs/base/release-risk-review.md
grep "skriver koden först" ~/ai-skill-library/packs/tdd/tdd.md
```
Expected: one match each.

- [ ] **Step 5: Commit**

```bash
cd ~/ai-skill-library
git add packs/light/session-discipline.md packs/base/release-risk-review.md packs/tdd/tdd.md
git commit -m "refactor: skärp vagt språk i session-discipline, release-risk-review och tdd"
```

---

### Task 4: Trim `python` pack

**Files:**
- Modify: `packs/python/python-review.md`
- Modify: `packs/python/script-review.md`

- [ ] **Step 1: Replace `python-review.md`**

Replace the entire file with:

```markdown
---
name: python-review
description: Use when reviewing Python code — checks idiomatic style, typing, error handling, and common pitfalls
---

# Python Review

- Använd `with`-statement för resurser (filer, connections)
- Fånga specifika exceptions — aldrig bara `except Exception` eller `except`
- Mutable default arguments (`def f(x=[])`) — använd `None` och sätt default i kroppen
- Typannotationer på parametrar och returvärde
- Funktioner gör en sak — dela upp om de blir längre än ~30 rader

## Fel att flagga
- Tyst fångst av exceptions utan loggning
- `print()` för felutskrift istället för `logging` eller `sys.stderr`
- Hårdkodade sökvägar som inte fungerar cross-platform
- `==` för `None`-jämförelse — använd `is None`
```

- [ ] **Step 2: Replace `script-review.md`**

Replace the entire file with:

```markdown
---
name: script-review
description: Use when reviewing Python CLI scripts — checks argument handling, exit codes, error output, and runnability
---

# Script Review

- `if __name__ == "__main__":` guard krävs
- Argument via `argparse` — inte manuell `sys.argv`-parsing
- Felaktig input → tydligt felmeddelande + exit 1, inte Python traceback
- Exit 0 framgång · exit 1 användarfel · exit 2+ systemfel
- Felmeddelanden på `sys.stderr`, framgång på `stdout`
- Shebang: `#!/usr/bin/env python3`

## Fel att flagga
- Saknad `if __name__ == "__main__"` guard
- Felmeddelanden på stdout istället för stderr
- `sys.exit()` anropas inte vid fel — scriptet "faller ut"
```

- [ ] **Step 3: Verify line counts**

```bash
wc -l ~/ai-skill-library/packs/python/python-review.md ~/ai-skill-library/packs/python/script-review.md
```
Expected: both under 20 lines.

- [ ] **Step 4: Commit**

```bash
cd ~/ai-skill-library
git add packs/python/python-review.md packs/python/script-review.md
git commit -m "refactor: trimma python-pack till concise style"
```

---

### Task 5: Trim `backend` pack

**Files:**
- Modify: `packs/backend/api-review.md`
- Modify: `packs/backend/db-review.md`

- [ ] **Step 1: Replace `api-review.md`**

Replace the entire file with:

```markdown
---
name: api-review
description: Use when reviewing REST API endpoints — checks design, error handling, validation, and authentication
---

# API Review

- All input valideras vid API-gränsen — lita aldrig på klientdata
- Autentisering krävs för skyddad data; auktorisering kontrolleras — äger användaren resursen?
- 500-fel loggas server-side — returnera aldrig stack traces till klienten
- Timeout-hantering för externa anrop

## Fel att flagga
- Exponering av känslig data i svar (lösenord, tokens, interna ID:n)
- Saknad autentisering på känsliga endpoints
- SQL/NoSQL-injection via ovaliderad input
- Ingen rate limiting på publika endpoints
```

- [ ] **Step 2: Replace `db-review.md`**

Replace the entire file with:

```markdown
---
name: db-review
description: Use when reviewing database schemas, queries, or migrations — checks correctness, performance, and security
---

# DB Review

- Inga N+1-problem — bulk-hämta relaterad data, inte en query per rad
- Parametriserade queries — aldrig string concatenation med användarinput
- Migrationer reversibla — down-migration finns
- Migrationer säkra mot livedatabas — undvik långa table locks
- Transaktioner: korta, samlade, minimera tid med lås

## Fel att flagga
- Rå SQL med användarinput (SQL-injection)
- Migration som droppar kolumn/tabell utan backup-plan
- Queries inuti loopar
- `SELECT *` i produktion
```

- [ ] **Step 3: Verify line counts**

```bash
wc -l ~/ai-skill-library/packs/backend/api-review.md ~/ai-skill-library/packs/backend/db-review.md
```
Expected: both under 20 lines.

- [ ] **Step 4: Commit**

```bash
cd ~/ai-skill-library
git add packs/backend/api-review.md packs/backend/db-review.md
git commit -m "refactor: trimma backend-pack till concise style"
```

---

### Task 6: Trim `frontend` pack

**Files:**
- Modify: `packs/frontend/component-review.md`

- [ ] **Step 1: Replace `component-review.md`**

Replace the entire file with:

```markdown
---
name: component-review
description: Use when reviewing React components — checks hooks rules, rendering issues, prop design, and side effects
---

# Component Review

- `useEffect` dependency array komplett — inga saknade beroenden
- Listor har stabil `key`-prop (inte index om ordning kan ändras)
- Cleanup-funktion i `useEffect` för subscriptions och timers
- Ingen prop drilling djupare än 2 nivåer

## Fel att flagga
- `useEffect` utan dependency array (körs varje render)
- State-mutationer direkt (`state.x = y` istället för `setState`)
- Asynkron funktion direkt som `useEffect`-callback
- Listor utan `key`-prop
```

- [ ] **Step 2: Verify line count**

```bash
wc -l ~/ai-skill-library/packs/frontend/component-review.md
```
Expected: under 20 lines.

- [ ] **Step 3: Commit**

```bash
cd ~/ai-skill-library
git add packs/frontend/component-review.md
git commit -m "refactor: trimma frontend-pack till concise style"
```
