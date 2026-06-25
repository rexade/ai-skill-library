# ai-skill-library

On-demand skills för Claude Code. Byt pack beroende på vad du jobbar med — agenten vet hur den ska jobba utan att du behöver förklara det varje gång.

```
plain      →  inga skills, råa prompts
light      →  grundläggande disciplin för allt arbete
embedded / robot / backend / ...  →  domänspecifikt
```

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
| `light` | session-discipline, verification-before-completion, code-review, security-baseline, context7-check, isolation | Allmänt bruk |
| `tdd` | tdd, verification-before-completion | Bygger ny kod med TDD |
| `embedded` | embedded-risk-review, hardware-signal-test, log-analysis, can-mqtt-debug, release-risk-review, verification-before-completion | Embedded-projekt |
| `robot` | robot-framework-review, robot-dryrun-check, test-data-quality, release-risk-review, verification-before-completion | Robot Framework-projekt |
| `ci` | ci-failure-analysis, build-repair-loop, test-log-triage, verification-before-completion | CI/CD-arbete |
| `security` | prompt-injection-check, security-baseline, verification-before-completion | Säkerhetsgranskning |
| `frontend` | component-review, security-baseline, verification-before-completion | React/frontend-arbete |
| `backend` | api-review, db-review, security-baseline, release-risk-review, verification-before-completion | API/databas/backend-arbete |
| `python` | python-review, script-review, verification-before-completion | Python-script och verktyg |

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

MCP-server för att hämta aktuell dokumentation för bibliotek och ramverk i realtid. **Obligatorisk** — eliminerar antaganden om API-format, protokoll och beteende innan du skriver kod. Utan Context7 kodar du mot vad du tror att dokumentationen säger.

```bash
claude mcp add context7 -- npx -y @upstash/context7-mcp
```

### code-simplifier

Plugin för att hålla kod enkel och undvika onödig komplexitet.

```bash
claude plugin add code-simplifier@claude-code-marketplace
```

> **Obs:** superpowers täcker brainstorming, planning och verification globalt. Packs i ai-skill-library komplettering med domänspecifika skills.

## Arbetsmetoden i praktiken — tre versioner jämförda

Vi byggde samma Python CLI-verktyg tre gånger parallellt:

| | Plain | Skills | Skills + Context7 |
|---|---|---|---|
| Design först | Nej | Ja | Ja |
| Tester | 0 | 12 | 13 |
| Korrekt regex-ordning | Okänd | Troligen fel | Verifierat rätt |
| Resursläcka | Nej | Ja | Nej |
| Källan till formatet | Antagande | Antagande | Dokumentation |

### Vad varje version lärde oss

**Plain:** Snabb, ren kod med typannotationer och korrekt resurshantering. Men utan tester — korrekthet obevisad, antaganden otestad.

**Skills:** Design-först-processen och TDD laddades automatiskt. 12 tester, verifierbart beteende. Men regex-ordningen antogs (passed före failed) utan att kontrollera pytest-dokumentationen — en bug som gömde sig i koden.

**Skills + Context7:** Context7 bekräftade exakt format från dokumentationen. RED-fasen i TDD exponerade omedelbart att regex-ordningen var fel. Buggen fixades *innan* koden ansågs klar. 13 tester, korrekt parsning.

### Lärdomen

> Context7 är inte ett nice-to-have — det eliminerar antaganden. Varje gång du integrerar mot ett externt format, protokoll eller API: verifiera mot dokumentationen först.

> TDD + Context7 är kombinationen som fångar bugs tidigt. TDD ensamt fångar bara det du vet att du ska testa.

**Skills styr processen rätt. Context7 säkerställer att processen utgår från fakta.**

## Guides

`guides/` innehåller metodikdokumentation för hur man jobbar strukturerat med AI:

| Fil | Innehåll |
|-----|----------|
| `vibe-coding-presentation.md` | Arbetsmetoden komplett — principer, säkerhet, konkreta spår för befintligt repo och nytt projekt |

## Uppdatera på ny maskin

```bash
cd ~/ai-skill-library && git pull
```
