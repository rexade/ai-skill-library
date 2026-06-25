---
name: component-review
description: Use when reviewing React components — checks hooks rules, rendering issues, prop design, and side effects
---

# Component Review

Granska React-komponenter innan de anses klara.

## Checklista

**Hooks**
- Inga hooks inuti conditionals, loopar eller nested functions
- `useEffect` har korrekt dependency array — inga saknade beroenden
- `useState` initieras med rätt typ
- Custom hooks börjar med `use`

**Props**
- Props är tydligt namngivna och minimala — komponenten tar inte emot mer än den behöver
- Callbacks heter `onX` (t.ex. `onClick`, `onChange`)
- Ingen prop drilling djupare än 2 nivåer — överväg context eller state management

**Rendering**
- Inga onödiga re-renders — memoize med `useMemo`/`useCallback` vid behov
- Listor har stabil `key`-prop (inte index om ordning kan ändras)
- Conditional rendering är tydlig och inte nästlad på mer än 2 nivåer

**Sidoeffekter**
- Datahämtning sker i `useEffect` eller via ett datahämtningsbibliotek (React Query, SWR)
- Cleanup-funktion finns i `useEffect` där det behövs (subscriptions, timers)
- Inga direkta DOM-manipulationer utan via refs

**Fel att flagga**
- `useEffect` utan dependency array (körs varje render)
- State-mutationer direkt (`state.x = y` istället för `setState`)
- Asynkron funktion direkt som `useEffect`-callback
