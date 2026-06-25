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
| `light` | session-discipline, verification, code-review, security-baseline | Allmänt bruk |
| `tdd` | tdd, verification | Bygger ny kod med TDD |
| `embedded` | embedded-risk-review, hw-signal, logs, CAN/MQTT, release-risk, verification | Embedded-projekt |
| `robot` | RF-review, dryrun, test-data, release-risk, verification | Robot Framework-projekt |
| `ci` | ci-failure, build-repair, log-triage, release-risk, verification | CI/CD-arbete |
| `security` | prompt-injection, security-baseline, verification | Säkerhetsgranskning |

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
