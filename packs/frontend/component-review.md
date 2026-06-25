---
name: component-review
description: Use when reviewing React components — checks hooks rules, rendering issues, prop design, and side effects
---

# Component Review

- `useEffect` dependency array komplett — inga saknade beroenden
- Listor har stabil `key`-prop (inte index om ordning kan ändras)
- Cleanup-funktion i `useEffect` för subscriptions och timers
- Ingen prop drilling djupare än 2 nivåer

## Fel att flagga
- `useEffect` utan dependency array (körs varje render)
- State-mutationer direkt (`state.x = y` istället för `setState`)
- Asynkron funktion direkt som `useEffect`-callback
- Listor utan `key`-prop
