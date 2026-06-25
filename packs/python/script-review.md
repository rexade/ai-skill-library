---
name: script-review
description: Use when reviewing Python CLI scripts — checks argument handling, exit codes, error output, and runnability
---

# Script Review

Granska Python CLI-script innan de anses klara.

## Checklista

**Struktur**
- Script har `if __name__ == "__main__":` guard
- Logik är separerad från CLI-hantering — lätt att testa utan att anropa scriptet
- Använd `argparse` (eller `click`/`typer`) för argument — inte manuell `sys.argv`-parsing

**Argument och input**
- Alla argument är dokumenterade med `help=`-text
- Obligatoriska vs valfria argument är tydliga
- Felaktig input ger tydligt felmeddelande och exit-kod 1 — inte en Python traceback

**Exit-koder**
- Exit 0 vid framgång
- Exit 1 vid användarfel (fel argument, fil saknas)
- Exit 2+ vid systemfel (permission denied, nätverksfel)
- `sys.exit()` anropas explicit — scriptet faller inte bara ut

**Felutskrifter**
- Felmeddelanden skrivs till `sys.stderr`, inte `stdout`
- Framgångsinformation skrivs till `stdout`
- Loggning med `logging`-modulen vid mer komplex output

**Körbarhet**
- Shebang-rad finns: `#!/usr/bin/env python3`
- Scriptet är körbart (`chmod +x`) om det ska köras direkt
- Beroenden är dokumenterade (requirements.txt eller pyproject.toml)

**Fel att flagga**
- Saknad `if __name__ == "__main__"` guard
- Felmeddelanden på stdout istället för stderr
- Exit utan exit-kod vid fel
- Hårdkodade filsökvägar eller konfigurationsvärden
