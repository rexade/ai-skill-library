---
name: embedded-risk-review
description: Use when reviewing embedded system code or test cases — checks hardware state, resource management, and timing
---

# Embedded Risk Review

## Hårdvarutillstånd
- Är hårdvarutillståndet kontrollerat och känt innan testet?
- Återställs hårdvaran till känt tillstånd efter testet (teardown)?
- Kan testet misslyckas av miljöskäl snarare än produktfel?

## Resurshantering
- Frigörs alla resurser (filer, sockets, CAN-bus, GPIO)?
- Finns risker för resource leaks vid timeout eller fel?

## Timing
- Innehåller koden hårdkodade sleep/delay som borde vara condition-baserade?
- Är timeouts rimliga för målhårdvaran?
- Kan race conditions uppstå?

## Klassificering
Om ett testfel uppstår — är det:
- **Produktfel:** Felet finns i produkten
- **Testfel:** Testet är felaktigt skrivet
- **Riggfel:** Testmiljön fungerar inte som förväntat
- **Infrastrukturfel:** CI, nätverk, verktyg

Klassificeringen avgör vem som äger felet.
