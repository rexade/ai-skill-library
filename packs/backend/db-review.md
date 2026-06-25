---
name: db-review
description: Use when reviewing database schemas, queries, or migrations — checks correctness, performance, and security
---

# DB Review

- Inga N+1-problem — bulk-hämta relaterad data, inte en query per rad
- Parametriserade queries — aldrig string concatenation med användarinput
- Migrationer reversibla — down-migration finns
- Migrationer säkra mot livedatabas — undvik långa table locks
- Transaktioner: korta, samlade, minimera tid med lås

## Fel att flagga
- Rå SQL med användarinput (SQL-injection)
- Migration som droppar kolumn/tabell utan backup-plan
- Queries inuti loopar
- `SELECT *` i produktion
