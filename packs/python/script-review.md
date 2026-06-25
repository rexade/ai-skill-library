---
name: script-review
description: Use when reviewing Python CLI scripts — checks argument handling, exit codes, error output, and runnability
---

# Script Review

- `if __name__ == "__main__":` guard krävs
- Argument via `argparse` — inte manuell `sys.argv`-parsing
- Felaktig input → tydligt felmeddelande + exit 1, inte Python traceback
- Exit 0 framgång · exit 1 användarfel · exit 2+ systemfel
- Felmeddelanden på `sys.stderr`, framgång på `stdout`
- Shebang: `#!/usr/bin/env python3`

## Fel att flagga
- Saknad `if __name__ == "__main__"` guard
- Felmeddelanden på stdout istället för stderr
- `sys.exit()` anropas inte vid fel — scriptet "faller ut"
