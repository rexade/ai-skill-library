# ai-skill-library

On-demand skills för Claude Code. Tre lägen: plain (inga skills), light (grundläggande), domain (projektspecifikt).

## Installation

```bash
git clone git@github.com:<ditt-användarnamn>/ai-skill-library.git ~/ai-skill-library
echo 'export PATH="$HOME/ai-skill-library/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

## Användning

```bash
ai-skills use light      # Aktivera light pack
ai-skills use embedded   # Aktivera embedded pack
ai-skills use tdd        # Aktivera TDD pack
ai-skills clear          # Ta bort aktiva skills
ai-skills status         # Visa aktivt pack och installerade skills
ai-skills list           # Lista tillgängliga packs
```

## Packs

| Pack | Skills | Använd när |
|------|--------|------------|
| `light` | session-discipline, verification-before-completion, code-review, security-baseline | Allmänt bruk |
| `tdd` | tdd, verification-before-completion | Bygger ny kod med TDD |
| `embedded` | embedded-risk-review, hardware-signal-test, log-analysis, can-mqtt-debug, release-risk-review, verification-before-completion | Embedded-projekt |
| `robot` | robot-framework-review, robot-dryrun-check, test-data-quality, release-risk-review, verification-before-completion | Robot Framework-projekt |
| `ci` | ci-failure-analysis, build-repair-loop, test-log-triage, release-risk-review, verification-before-completion | CI/CD-arbete |
| `security` | prompt-injection-check, security-baseline, verification-before-completion | Säkerhetsgranskning |

> **Obs:** Planning/brainstorming täcks av `superpowers:brainstorming` globalt.

## Lägg till i `.gitignore` för dina projekt

```gitignore
.claude/skills/
.claude/active-skills.txt
```

## Uppdatera på ny maskin

```bash
cd ~/ai-skill-library && git pull
```
