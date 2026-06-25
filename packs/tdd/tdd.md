---
name: tdd
description: Use when implementing a feature or bugfix — write the test before the code
---

# Test-Driven Development

**Skriv testet innan koden.**

## Cykeln

1. **Red** — skriv testet, kör det, se det misslyckas
2. **Green** — skriv minsta möjliga kod som gör testet grönt
3. **Refactor** — städa upp medan testerna är gröna

## Varför i den ordningen

Ett test som aldrig har misslyckats bevisar ingenting — det kan vara felskrivet eller alltid returnera true. Att se det misslyckas är kvittot på att det testar rätt sak.

## Vanliga genvägar att undvika

| Tanke | Problem |
|-------|---------|
| "Det är för enkelt för ett test" | Enkla saker har buggar också |
| "Jag testar efteråt" | Tester-efteråt verifierar bara det du vet — inte det du missat |
| "Jag vet hur det ska fungera" | Vetande ≠ bevis |
| "Jag skriver koden först och lägger till tester efteråt" | Tester-efteråt verifierar bara det du vet — inte det du missat |
