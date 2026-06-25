---
name: isolation
description: Use when starting any task with shell access — enforces project boundary and prevents credential exposure
---

# Isolation

Stanna innanför projektmappen. Läs, skriv och kör bara det som hör till projektet.

## Håll dig borta från

- `~/.ssh/`, `~/.aws/`, `~/.env` (hemkatalogen), `~/.netrc`, `~/.gnupg/`, `/etc/`
- `printenv` / `env` / `set` — dumpar miljöhemligheter
- `find ~` eller `ls ~` — söker utanför projektet

## Fråga innan

- Åtgärder utanför projektmappen
- `git push`, commit till main, deploy, restart av tjänster
- Destruktiva kommandon (`rm -rf`, `truncate`, `drop`)

Bypass permission är på — det finns ingen dialog som nät. Om du är osäker: fråga.
