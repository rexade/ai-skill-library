# claude-md-check Skill — Design Spec

Date: 2026-06-25

## Goal

Add a `claude-md-check` skill to the `base` pack that bootstraps a minimal `CLAUDE.md` the first time Claude enters a repo that doesn't have one. The user will never write `CLAUDE.md` manually — this skill ensures it always exists.

## Trigger

Skill activates only when `CLAUDE.md` does not exist in the project root. If `CLAUDE.md` exists: skill is completely silent.

## Behaviour

1. Detect missing `CLAUDE.md`
2. Ask the user one question: *"Vad kör projektet på och finns det regler jag ska veta?"*
3. Write `CLAUDE.md` from the answer
4. Continue the session normally

## Output Format

```markdown
# [current directory name]

## Stack
[from answer]

## Kommandon
[from answer, or "okänt ännu"]

## Regler
[from answer, or "ingen ännu"]
```

Short, rules-based, not prose. No project description, no history, no filler.

## Placement

- File: `packs/base/claude-md-check.md`
- Pack: `base` (always loaded regardless of active pack)

## Out of scope

- Updating or verifying an existing `CLAUDE.md` (that's `session-discipline`)
- Generating stack-specific boilerplate beyond `CLAUDE.md`
- Asking more than one question

## Files changed

| File | Change |
|---|---|
| `packs/base/claude-md-check.md` | New skill file |
