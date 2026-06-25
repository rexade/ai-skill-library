# ai-skill-library

On-demand skills för Claude Code. Tre lägen: plain (inga skills), light (grundläggande), domain (projektspecifikt).

## Installation

```bash
git clone https://github.com/rexade/ai-skill-library.git ~/ai-skill-library
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
| `fullstack` | component-review, api-review, db-review, security-baseline, release-risk-review, verification-before-completion | Frontend/backend/fullstack-projekt |

> **Obs:** Planning/brainstorming täcks av `superpowers:brainstorming` globalt.

## Lägg till i `.gitignore` för dina projekt

```gitignore
.claude/skills/
.claude/active-skills.txt
```

## Rekommenderade plugins

Dessa tre plugins ska alltid vara installerade och aktiva i kombination med ai-skill-library.

### superpowers

Officiellt plugin som ger brainstorming, TDD, verification-before-completion och fler workflows.

```bash
claude plugin add superpowers@claude-plugins-official
```

### context7

MCP-server för att hämta aktuell dokumentation för bibliotek och ramverk i realtid.

```bash
claude mcp add context7 -- npx -y @upstash/context7-mcp
```

### code-simplifier

Plugin för att hålla kod enkel och undvika onödig komplexitet.

```bash
claude plugin add code-simplifier@claude-code-marketplace
```

> **Obs:** superpowers täcker brainstorming, planning och verification globalt. Packs i ai-skill-library komplettering med domänspecifika skills.

## Uppdatera på ny maskin

```bash
cd ~/ai-skill-library && git pull
```
