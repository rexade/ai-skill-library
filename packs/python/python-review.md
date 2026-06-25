---
name: python-review
description: Use when reviewing Python code — checks idiomatic style, typing, error handling, and common pitfalls
---

# Python Review

- Använd `with`-statement för resurser (filer, connections)
- Fånga specifika exceptions — aldrig bara `except Exception` eller `except`
- Mutable default arguments (`def f(x=[])`) — använd `None` och sätt default i kroppen
- Typannotationer på parametrar och returvärde
- Funktioner gör en sak — dela upp om de blir längre än ~30 rader

## Fel att flagga
- Tyst fångst av exceptions utan loggning
- `print()` för felutskrift istället för `logging` eller `sys.stderr`
- Hårdkodade sökvägar som inte fungerar cross-platform
- `==` för `None`-jämförelse — använd `is None`
