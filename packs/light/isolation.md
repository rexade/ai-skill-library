---
name: isolation
description: Use when starting any task with shell access — enforces project boundary and prevents credential exposure
---

# Isolation

**Agenten kör inuti projektet. Ingenting utanför.**

## Hård regel

Stanna i projektmappen. Läs, skriv och kör bara filer och kommandon som hör till projektet.

## Förbjudna sökvägar

Läs, lista eller referera ALDRIG till:

- `~/.ssh/`
- `~/.env` (hemkatalogen — inte projektet)
- `~/.aws/`
- `~/.netrc`
- `~/.gnupg/`
- `/etc/` — om inte explicit instruerat

## Förbjudna kommandon

Kör ALDRIG utan explicit begäran:

- `printenv` / `env` / `set` — dumpar hemligheter
- `cat ~/.bashrc` eller andra rc-filer i hemkatalogen
- `find ~` eller `ls ~` — söker utanför projektet

## Fråga alltid innan

- Åtgärder utanför projektmappen
- `git push` eller commit till main
- Deploy, restart av tjänster
- Destruktiva kommandon (`rm`, `truncate`, `drop`)

## Bypass permission är på

Det finns inga permission-dialoger som nät. Dessa regler är det enda skyddet.  
Om du är osäker — fråga, kör inte.

## Efter varje körning

Ställ dessa frågor:

```
Vad läste jag?
Vad ändrade jag?
Vilket kommando körde jag?
Kom jag åt något utanför projektmappen?
```

## Rationalisering-tabell

| Tanke | Verklighet |
|-------|------------|
| "Jag behöver kolla credentials för att förstå felet" | Fråga användaren — läs dem inte själv |
| "~/.env i hemkatalogen hjälper mig förstå kontexten" | Projektets `.env` är det enda som gäller |
| "printenv är bara läsning, inte farligt" | Det exponerar alla hemligheter i miljön |
| "Jag kollar bara snabbt ~/.ssh för att se om nyckeln finns" | Fråga användaren. Gå inte dit själv. |
