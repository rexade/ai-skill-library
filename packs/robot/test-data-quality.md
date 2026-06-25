---
name: test-data-quality
description: Use when reviewing or creating test data for Robot Framework or embedded tests
---

# Test Data Quality

## Realism
- Är testdata representativ för produktionsdata?
- Täcker testdata gränsvärden? (min, max, typiskt, ogiltigt)
- Undviks "magiska" värden utan förklaring?

## Isolering
- Är testdata isolerad från andra tester?
- Delar tester testdata på ett sätt som skapar beroenden?
- Återställs testdata efter varje test (teardown)?

## Underhållbarhet
- Är testdata definierad på ett ställe (ej duplicerad)?
- Är det tydligt varför specifika värden valts?
- Påverkas testdata av ändringar i produkten?

## Robot Framework-specifikt
- Definieras testdata i Variables-sektionen?
- Används `Set Suite Variable` / `Set Test Variable` korrekt?
- Importeras testdata från filer för komplexa dataset?
