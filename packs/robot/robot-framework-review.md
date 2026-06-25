---
name: robot-framework-review
description: Use when reviewing Robot Framework test cases — checks structure, keywords, and test design quality
---

# Robot Framework Review

## Teststruktur
- Har testet tydlig Setup och Teardown?
- Är testet självständigt? (kan köras i valfri ordning)
- Är testet deterministiskt? (ger samma resultat varje gång)

## Keywords
- Är keywords på rätt abstraktionsnivå? (beskriver VAD, inte HUR)
- Är keyword-namn läsbara som engelska meningar?
- Återanvänds keywords eller dupliceras logik?

## Testdesign
- Testar testet ett enda beteende?
- Är assertions specifika? (ej bara `Should Be True`)
- Är felmeddelanden informativa vid testfel?

## Vanliga problem
- Hårdkodade sleep istället för `Wait Until Keyword Succeeds`
- Globala variabler som delar tillstånd mellan tester
- Setup som gömmer kritisk logik för testet
- Tester som alltid passerar oavsett produkttillstånd
