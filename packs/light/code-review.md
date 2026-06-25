---
name: code-review
description: Use when reviewing code changes — checks logic, edge cases, naming, and testability
---

# Code Review

## Korrekthet
- Löser koden det faktiska problemet?
- Hanteras edge cases? (tom input, null, stora värden, felfall)
- Kan koden misslyckas tyst? (undantag som sväljs, fel som ignoreras)

## Testbarhet
- Är koden testbar som den är skriven?
- Finns tester för det som ändrades?
- Täcker testerna happy path och felfall?

## Läsbarhet
- Är namngivning tydlig och konsekvent?
- Gör koden vad den verkar göra?
- Behövs kommentarer för icke-uppenbar logik?

## Säkerhet
- Hanteras input från externa källor säkert?
- Exponeras inga hemligheter i loggar eller felmeddelanden?

## Rapportera som

**Kritisk:** Buggar, säkerhetshål, kraschar — måste fixas  
**Viktig:** Testgap, namnproblem, logikfel — bör fixas  
**Minor:** Stil, formatering — kan fixas

Avsluta med: ✅ Godkänd / ❌ Inte godkänd — och varför.
