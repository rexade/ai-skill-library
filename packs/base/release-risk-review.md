---
name: release-risk-review
description: Use before releasing or deploying to production — assesses what can go wrong and whether rollback is possible
---

# Release Risk Review

## Vad kan gå sönder?
- Vilka komponenter påverkas av denna release?
- Finns beroenden på extern hårdvara, firmware, eller tjänster?
- Kan felet yttra sig fördröjt (ej direkt vid driftsättning)?

## Reversibilitet
- Kan releasen rullas tillbaka?
- Påverkar releasen persistent state (databas, firmware, konfiguration)?
- Om rollback krävs — hur lång tid tar det?

## Verifiering i produktion
- Vad är det första tecknet på att releasen är OK?
- Vad är det första tecknet på att något gick fel?
- Vem ska monitorera och under hur lång tid? (Minst under första körningen i produktion)

## Godkännande
Svara explicit: **Redo att releasa / Inte redo** — och varför.
