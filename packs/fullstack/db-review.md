---
name: db-review
description: Granska databasscheman, queries och migrationer för korrekthet, prestanda och säkerhet
---

# DB Review

Granska databasrelaterad kod innan den anses klar.

## Checklista

**Schema**
- Relationer har foreign keys med rätt ON DELETE/ON UPDATE-beteende
- Index finns på kolumner som används i WHERE, JOIN och ORDER BY
- Kolumntyper matchar datan — inte `TEXT` där `VARCHAR(n)` räcker
- NOT NULL där fältet alltid ska ha ett värde

**Queries**
- Inga N+1-problem — bulk-hämta relaterad data istället för en query per rad
- Queries använder parametriserade värden — aldrig string concatenation med användarinput
- SELECT hämtar bara kolumner som används, inte `SELECT *` i produktion
- Tunga queries har EXPLAIN-analys eller är testade med realistisk datamängd

**Migrationer**
- Migrationen är reversibel (down-migration finns)
- Migrationen är säker att köra på en livedatabas — undvik långa table locks
- Befintlig data hanteras korrekt vid schema-ändringar
- Migrationen är testad mot en kopia av produktionsdata om möjligt

**Transaktioner**
- Operationer som måste lyckas tillsammans wrappas i en transaktion
- Transaktioner hålls korta — minimera tid med lås

**Fel att flagga**
- Rå SQL med användarinput (SQL-injection)
- Migration som droppar kolumn/tabell utan backup-plan
- Saknade index på ofta filtrerade kolumner
- Queries inuti loopar
