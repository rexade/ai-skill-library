---
name: hardware-signal-test
description: Use when verifying hardware signals, CAN messages, or MQTT payloads in tests
---

# Hardware Signal Test

## Innan signalverifiering
- Är hårdvaran i rätt tillstånd för att generera signalen?
- Väntar testet på signal med condition-based waiting (ej sleep)?

## Signalvalidering
- Verifieras värdet, inte bara att signalen existerar?
- Är toleranser explicita? (±5% eller exakt?)
- Täcks edge cases? (min-värde, max-värde, ogiltigt värde)

## Condition-based waiting — ej sleep

Skriv aldrig:
```python
time.sleep(2)
assert signal_received()
```

Skriv istället:
```python
wait_until(signal_received, timeout=5)
assert signal_received()
```
