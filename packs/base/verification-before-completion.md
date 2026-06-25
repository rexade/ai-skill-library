---
name: verification-before-completion
description: Use before claiming any task is complete — requires fresh evidence before claims
---

# Verification Before Completion

**Inga påståenden utan bevis.**

## Innan du säger att något är klart

1. Kör testerna — se faktisk output
2. Kör linter — se faktisk output
3. Granska diff — vad ändrades egentligen?

## Förbjudna fraser utan att ha kört verifieringen

- "Det borde fungera"
- "Ser rätt ut"
- "Testerna passerar nog"
- "Klart"

## Regeln

Kör kommandot. Läs outputen. Sedan påstå resultatet.

Kravet: faktisk testkörning i detta meddelande — inte en tidigare körning.
