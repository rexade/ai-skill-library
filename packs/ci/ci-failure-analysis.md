---
name: ci-failure-analysis
description: Use when a CI pipeline fails — distinguishes flaky tests from real failures and finds root cause
---

# CI Failure Analysis

## Är det tillfälligt eller strukturellt?

1. Kör om jobbet utan ändringar
2. Om det passerar: sannolikt flaky test eller miljöproblem
3. Om det misslyckas igen: strukturellt fel — undersök rotorsak

## Klassificera felet

| Typ | Tecken | Åtgärd |
|-----|--------|--------|
| Flaky test | Slumpmässigt pass/fail, inga kodändringar | Isolera och fixa testet |
| Miljöproblem | Misslyckas i CI men inte lokalt | Jämför miljöer |
| Regressionsbug | Misslyckas sedan specifik commit | `git bisect` |
| Infrastrukturproblem | Timeout, nätverksfel, disk full | Ops-team |

## Undersökningsordning
1. Läs felmeddelandet — exakt rad, exakt fel
2. Kolla loggarna bakåt från felet
3. Jämför med senaste gröna körning
4. Isolera till minsta möjliga reproducerbara fall
