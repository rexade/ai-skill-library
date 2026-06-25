---
name: tdd
description: Use when implementing any feature or bugfix — enforces red-green-refactor before writing production code
---

# Test-Driven Development

**Skriv testet innan koden. Alltid.**

## Cykeln

### 🔴 Red — skriv ett misslyckande test
- Skriv testet för beteendet du vill implementera
- Kör det — det MÅSTE misslyckas
- Om det passerar direkt: testet testar ingenting, skriv om det

### 🟢 Green — minimal kod för att klara testet
- Skriv minsta möjliga kod som gör testet grönt
- Kör testet — det MÅSTE passera
- Motstå frestelsen att generalisera nu

### 🔵 Refactor — städa utan att bryta
- Förbättra koden medan testerna är gröna
- Kör testerna efter varje ändring
- Om något går rött: ångra och försök igen

## Järnlagen

```
INGET PRODUKTIONSKOD UTAN ETT MISSLYCKANDE TEST FÖRST
```

Inga undantag. Inte för "enkla saker". Inte för "det är bara en rad".

## Vanliga rationaliseringar

| Ursäkt | Verklighet |
|--------|------------|
| "Det är för enkelt" | Enkla saker har buggar också |
| "Jag vet hur det ska fungera" | Vetande ≠ bevis |
| "Testet tar för lång tid" | Debuggning tar längre tid |
