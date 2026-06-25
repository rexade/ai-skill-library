---
name: session-discipline
description: Use when starting or ending a session — enforces single-goal sessions and session wrap
---

# Session Discipline

**En session = ett mål.**

## Sessionstart

1. Finns `progress.md`? Läs den och ta vid där.
2. Kontrollera att `CLAUDE.md` stämmer med projektets nuläge
3. Definiera ett konkret mål för sessionen — inte "gör allt"

## Under sessionen

- Jobba mot ett mål — stäng sessionen när det är klart
- Om du gjort mer än ett oplanerat kontextbyte under sessionen: stäng och starta om med ett tydligt mål

## Sessionavslut

1. Kör tester
2. Committa pågående arbete
3. Uppdatera progress-fil om det finns en
4. Stäng sessionen

**Regeln:** Långa sessioner driftar. Korta sessioner med tydliga mål ger stabila resultat.

## Scope Calibration

Skills stödjer omdöme — de ersätter det inte.

| Uppgift | Process |
|---|---|
| Trivial: 1 fil, tydlig brief | Implementera direkt. Ingen brainstorming, ingen spec. |
| Liten: 2–5 filer, klar riktning | Kort designcheck, sedan implementera inline. |
| Medium/stor: 6+ filer, oklart, arkitekturellt, riskfyllt | Full brainstorming → spec → plan → subagents. |

**verification-before-completion körs alltid** — oavsett storlek.
