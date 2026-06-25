---
name: build-repair-loop
description: Use when a build is broken — isolates the failure and repairs it systematically without introducing new issues
---

# Build Repair Loop

**Principen:** Isolera → Reproducera → Fixa → Verifiera → Commit

## Steg

### 1. Isolera
- Vilket exakt kommando misslyckas?
- Finns felet lokalt? I CI? Båda?
- Sedan vilken commit? (`git bisect` om oklart)

### 2. Minsta reproducerbara fall
- Kan du reproducera felet med en enda fil eller ett enda kommando?
- Minska scope tills du vet exakt vad som orsakar det

### 3. Fixa
- Fixa en sak i taget
- Kör bygget efter varje ändring
- Committa inte förrän bygget är grönt

### 4. Verifiera
- Kör hela test-suiten — ej bara det som var trasigt
- Kör linter
- Bekräfta att CI-pipeline är grön

### 5. Post-mortem (om allvarligt)
- Varför gick det sönder?
- Hur hindrar vi det nästa gång?
