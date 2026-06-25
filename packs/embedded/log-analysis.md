---
name: log-analysis
description: Use when analysing logs from embedded systems or test runs to find root causes
---

# Log Analysis

## Vad ska fångas
- Fångas loggar vid testfel automatiskt?
- Inkluderas timestamps?
- Loggas hårdvarutillstånd (ej bara mjukvara)?

## Vad ska sökas i loggar
1. **Fel och undantag** — sök på ERROR, EXCEPTION, FATAL, Traceback
2. **Timeouts** — sök på timeout, timed out, expired
3. **Tillståndsövergångar** — vad hände precis innan felet?
4. **Resursbrister** — memory, disk, connection refused

## Rotorsaksanalys
- Vad är det första felet i loggsekvensen? (inte det sista)
- Upprepas felet eller är det engångsfel?
- Korrelerar felet med en specifik hårdvara eller miljö?
