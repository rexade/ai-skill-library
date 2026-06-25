---
name: python-review
description: Granska Python-kod för idiomatisk stil, typing, felhantering och vanliga fallgropar
---

# Python Review

Granska Python-kod innan den anses klar.

## Checklista

**Stil och idiom**
- Använd list/dict/set comprehensions istället för loopar där det är tydligare
- Använd `enumerate()` istället för `range(len(x))`
- Använd `with`-statement för resurser (filer, connections)
- Föredra f-strings framför `.format()` eller `%`
- Funktioner gör en sak — dela upp om de blir längre än ~30 rader

**Typing**
- Funktioner har typannotationer på parametrar och returvärde
- Använd `Optional[X]` eller `X | None` (Python 3.10+) för värden som kan vara None
- Använd `list[X]`, `dict[K, V]`, `tuple[X, ...]` från inbyggda typer (Python 3.9+)
- Komplexa typer definieras som `TypeAlias` eller `dataclass`

**Felhantering**
- Fånga specifika exceptions, aldrig bara `except Exception` eller bara `except`
- Exceptions propageras uppåt om de inte kan hanteras meningsfullt lokalt
- Felmeddelanden är informativa och inkluderar relevant kontext
- Resurser stängs även vid fel (via `with` eller `finally`)

**Vanliga fallgropar**
- Mutable default arguments (`def f(x=[])`) — använd `None` och sätt default i funktionskroppen
- Sen bindning i lambdas inuti loopar
- `==` vs `is` — använd `is` bara för `None`, `True`, `False`
- Modifiering av lista/dict under iteration

**Fel att flagga**
- Tyst fångst av exceptions utan loggning
- `print()` för felutskrift istället för `logging` eller `sys.stderr`
- Hårdkodade sökvägar som inte fungerar cross-platform
