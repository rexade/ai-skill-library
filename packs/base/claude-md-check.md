---
name: claude-md-check
description: Use at the start of every session — creates CLAUDE.md if it doesn't exist so the project always has a work contract for the AI
---

# CLAUDE.md Check

Om `CLAUDE.md` saknas i projektroten: detta är ett nytt repo utan arbetskontrakt.

**Gör så här:**

1. Fråga: *"Vad kör projektet på och finns det regler jag ska veta?"*
2. Skriv `CLAUDE.md` baserat på svaret:

```markdown
# [katalognamn]

## Stack
[svar]

## Kommandon
[svar eller "okänt ännu"]

## Regler
[svar eller "ingen ännu"]
```

3. Fortsätt sessionen.

Om `CLAUDE.md` finns: gör ingenting.
