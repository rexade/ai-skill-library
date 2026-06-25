---
name: api-review
description: Use when reviewing REST API endpoints — checks design, error handling, validation, and authentication
---

# API Review

- All input valideras vid API-gränsen — lita aldrig på klientdata
- Autentisering krävs för skyddad data; auktorisering kontrolleras — äger användaren resursen?
- 500-fel loggas server-side — returnera aldrig stack traces till klienten
- Timeout-hantering för externa anrop

## Fel att flagga
- Exponering av känslig data i svar (lösenord, tokens, interna ID:n)
- Saknad autentisering på känsliga endpoints
- SQL/NoSQL-injection via ovaliderad input
- Ingen rate limiting på publika endpoints
