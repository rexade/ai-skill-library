---
name: can-mqtt-debug
description: Use when debugging CAN bus or MQTT communication issues in embedded test environments
---

# CAN/MQTT Debug

## CAN Bus

### Kontrollera bus-status
- Är bussen aktiv? (ej bus-off)
- Är bitrate korrekt konfigurerad?
- Finns termineringsresistor?

### Meddelandeanalys
- Korrekt CAN-ID?
- Korrekt DLC (data length)?
- Är signalernas bit-position och endianness rätt?
- Är värdet inom giltigt range?

## MQTT

### Anslutning
- Är broker åtkomlig?
- Är topic rätt? (case-sensitive)
- Är QoS rätt för use-caset?

### Payload
- Är payload i rätt format? (JSON, binary, string)
- Är encoding rätt? (UTF-8)

## Felsökningsordning
1. Bus/broker online?
2. Rätt topic/ID?
3. Rätt format?
4. Rätt värde?
