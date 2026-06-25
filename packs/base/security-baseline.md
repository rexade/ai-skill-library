---
name: security-baseline
description: Use when an agent has shell access, file access, or calls external APIs — checks for injection and privilege risks
---

# Security Baseline

Ställ dessa frågor vid varje agentkörning:

## Prompt Injection
- Läste agenten opålitligt innehåll? (PR-kommentarer, README, PDFs, e-post)
- Kunde fientlig input ha styrt agentens beteende?

## Filåtkomst
- Nådde agenten bara projektmappen? Håll dig borta från `~/.ssh/`, `~/.aws/`, `~/.env`

## Behörigheter
- Körde agenten med minsta nödvändiga behörighet?
- Kördes deployer eller farliga kommandon utan explicit instruktion?

## Bevis
- Vad läste agenten?
- Vad ändrade agenten?
- Vilket kommando körde agenten?

**Låt aldrig bekvämlighet springa ifrån isolering.**
