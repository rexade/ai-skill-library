---
name: test-log-triage
description: Use when triaging test logs from CI or embedded test runs to prioritize what to investigate
---

# Test Log Triage

## Prioriteringsordning

1. **Assertions som failar** — produkt-buggar eller test-buggar
2. **Exceptions och crashes** — allvarliga fel
3. **Timeouts** — miljö- eller timing-problem
4. **Warnings** — kan vara förvarningstecken

## Sök dessa mönster

```bash
# Fel och undantag
grep -iE "ERROR|EXCEPTION|FATAL|FAIL|Traceback" test.log

# Timeouts
grep -iE "timeout|timed out|expired" test.log

# Resursproblem
grep -iE "no space|out of memory|connection refused" test.log
```

## Vad ska rapporteras

- Antal misslyckade tester (ej bara "det gick fel")
- Första felet i loggsekvensen — inte det sista
- Är felen relaterade eller oberoende?
- Reproducerbart eller engångsfel?
