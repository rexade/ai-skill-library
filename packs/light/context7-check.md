---
name: context7-check
description: Använd när uppgiften involverar externa bibliotek, API:er, filformat eller protokoll — slå upp dokumentationen i Context7 innan implementation börjar
---

# Context7 Check

Innan du skriver kod som beror på ett externt bibliotek, API, filformat eller protokoll: **slå upp det i Context7 först**.

## När detta gäller

- Parsning av format med specificerat schema (pytest-output, JSON-schema, XML, CSV-dialekter)
- Anrop mot externa API:er eller SDK:er
- Användning av ett bibliotek du inte använde senast för 6+ månader sedan
- Alla antaganden om versionsberoende beteende

## Gör så här

1. Identifiera vad i uppgiften som beror på extern dokumentation
2. Slå upp det med Context7 innan du börjar koda
3. Notera exakt format, metoder eller beteende som bekräftats
4. Koda mot det bekräftade — inte mot vad du tror att du minns

## Varför

I ett jämförelsetest byggde två instanser samma pytest-logganalysator. Båda antog att pytest skriver `passed` före `failed` i sammanfattningsraden. Context7 bekräftade det exakta formatet — och avslöjade att antagandet var fel. Den version som använde Context7 fångade buggen i RED-fasen. De andra fick fel parsning utan att veta om det.

**Antaganden om format kostar mer att fixa i produktion än att slå upp i dokumentationen tar.**
