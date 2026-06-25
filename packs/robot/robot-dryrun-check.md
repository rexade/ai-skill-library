---
name: robot-dryrun-check
description: Use before running Robot Framework tests — validates syntax without executing against hardware
---

# Robot Framework Dry-Run Check

Kör alltid dry-run innan testkörning mot hårdvara:

```bash
robot --dryrun <test-fil-eller-mapp>
```

## Vad dry-run kontrollerar
- Syntaxfel i `.robot`-filer
- Saknade keywords (ej definierade)
- Ogiltiga argument till keywords
- Import-fel (Libraries, Resources)

## Vad dry-run INTE kontrollerar
- Logik (testet kan fortfarande misslyckas)
- Hårdvarutillstånd
- Runtime-fel

## Tolka output
- `0 tests, 0 errors` → syntax OK, kör mot hårdvara
- `ERROR` i output → fixa innan körning
- `WARN` i output → kontrollera om det är allvarligt

**Kör alltid dry-run. Spara tid mot hårdvara.**
