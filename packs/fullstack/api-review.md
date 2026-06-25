---
name: api-review
description: Granska REST API-endpoints för korrekt design, felhantering, validering och autentisering
---

# API Review

Granska backend API-endpoints innan de anses klara.

## Checklista

**Design**
- HTTP-metod matchar operationen: GET (läs), POST (skapa), PUT/PATCH (uppdatera), DELETE (ta bort)
- Statuskoder är korrekta: 200 OK, 201 Created, 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found, 500 Internal Server Error
- URL-struktur är resursbaserad och konsekvent (`/users/:id` inte `/getUser?id=x`)
- Svar har konsekvent format (t.ex. alltid `{ data, error }`)

**Validering**
- All input valideras vid API-gränsen — lita aldrig på klientdata
- Felmeddelanden är informativa men avslöjar inte intern implementation
- Query-parametrar och path-parametrar valideras och sanitiseras

**Autentisering & auktorisering**
- Endpoint kräver autentisering om den hanterar skyddad data
- Auktorisering kontrolleras — användaren äger/har rätt till resursen
- JWT/session valideras på rätt sätt

**Felhantering**
- Try/catch runt databasanrop och externa tjänster
- 500-fel loggas server-side, returnerar inte stack traces till klienten
- Timeout-hantering för externa anrop

**Fel att flagga**
- Exponering av känslig data i svar (lösenord, tokens, interna ID:n)
- Saknad autentisering på känsliga endpoints
- SQL/NoSQL-injection via ovaliderad input
- Ingen rate limiting på publika endpoints
