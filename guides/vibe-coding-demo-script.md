# Vibe Coding — Live Demo Script

> **App:** Bug Report Formatter — användaren klistrar in röriga bugg-anteckningar och får ut en strukturerad bug report via Claude API.
>
> **Tid:** ~20 minuter
>
> **Format per steg:**
> - **Gör:** vad du gör på skärmen
> - **Säg:** vad du säger till publiken
> - **Skärmen:** vad publiken ser

---

## Förberedelser (innan presentationen)

- Claude Code installerat och inloggat
- Terminal öppen i `/home/henrik/`
- `bug-report-formatter/` finns redan byggd — används om live-bygget tar för lång tid
- Backup: `claude --version` bekräftar att Claude Code är inloggat

---

## Steg 1: Problemet (2 min)

**Säg:**
> "Vi har ett konkret problem. Jag hittade det i mitt eget arbete. När man rapporterar en bugg ser anteckningarna ofta ut såhär:"

**Gör:** Visa det här i terminalen eller på en slide:

```
login knappen funkar inte på mobil
testade iphone 13, chrome
klickar men inget händer
funkar på desktop
```

**Säg:**
> "Det räcker för att du ska förstå problemet — men det är inte en bug report. Steg ett i vibe coding: vi börjar med ett riktigt problem, inte en teknisk spec."

---

## Steg 2: Presentera idén för AI:n (3 min)

**Gör:** Öppna Claude Code i terminalen:

```bash
claude
```

**Säg:**
> "Lägg märke på vad som händer när jag startar en ny session. AI:n läser automatiskt minnet — den vet vad som är halvfärdigt, vad jag föredrar, hur jag jobbar. Jag behöver inte orientera den från scratch varje gång."

**Skärmen:** Session-start körs automatiskt, minnet laddas.

**Gör:** Skriv detta (eller liknande, i naturligt språk):

```
Jag vill bygga en liten webbapp. Användaren klistrar in röriga 
bugg-anteckningar och får tillbaka en strukturerad bug report. 
Tänker Python-backend med FastAPI och en enkel HTML-sida. 
Kan du hjälpa mig planera det?
```

**Säg:**
> "Observera — jag skriver inte kod. Jag förklarar problemet som för en kollega. AI:n börjar nu ställa frågor och tänka tillsammans med mig."

**Skärmen:** AI:n svarar med frågor eller förslag. Låt den köra klart.

**Säg:**
> "Det här är brainstorming-fasen. Ordningen spelar roll: förstå problemet, planera, implementera — inte tvärtom."

---

## Steg 3: Planera (3 min)

**Gör:** Be AI:n skriva en plan:

```
Skriv en implementation plan för det här. Bryt ner det i 
konkreta tasks med tydliga steg.
```

**Skärmen:** AI:n genererar en plan med tasks, filstruktur och beroenden.

**Säg:**
> "Nu vet AI:n vad den ska bygga — och i vilken ordning. Det här är planen som styr allt som kommer härnäst. Utan den jobbar AI:n i blindo och du vet inte om den gör rätt sak."

**Peka på planen och visa:**
> "Tre tasks. Varje task har en tydlig input och output. Ingen AI-agent behöver veta mer än sin del."

---

## Steg 3b: Sessioner och context (2 min)

**Säg:**
> "Nu gör vi något som känns konstigt — vi stänger sessionen."

**Gör:** Avsluta Claude Code (`exit` eller Ctrl+C).

**Säg:**
> "En session lever och dör med sin kontext. Ju längre den pågår, desto mer börjar AI:n tappa tråden — det kallas drift. Lösningen är inte att kämpa emot det. Lösningen är loopar."

**Gör:** Öppna en ny session:

```bash
claude
```

**Säg:**
> "Ny session. AI:n har glömt allt från förra sessionen — men planen finns kvar på disk. Vi ger den ett enda fokuserat mål: implementera task 1."

**Skärmen:** Ny session, AI:n läser planen och fortsätter direkt.

---

## Steg 4: Implementera (4 min)

**Säg:**
> "Nu kör vi. Jag ber Claude Code att implementera planen med separata subagenter — en per task."

**Gör:** Skriv i Claude Code:

```
Implementera den här planen med subagent-driven development.
```

**Skärmen:** Subagenter startar. Du ser dem implementera, testa och committa ett steg i taget.

**Säg (medan det kör):**
> "Varje subagent har ett smalt ansvar och ett rent kontextfönster. Den som bygger backend vet inte om frontend. Precis som i ett riktigt team."

**Säg:**
> "Efter varje task kör en reviewer och kontrollerar att det som byggdes stämmer med planen — inte mer, inte mindre. Det är kvalitetsgrindar: koden granskas innan vi går vidare. Samma princip som tester, lint och security scan — men inbyggt i flödet."

**Skärmen:** Reviewer-agenten rapporterar. Eventuella fynd fixas innan nästa task startar.

**Om det tar lång tid:** Visa det redan byggda projektet i `bug-report-formatter/` och förklara att det här är resultatet.

---

## Steg 5: Visa resultatet (2 min)

**Gör:** Starta appen:

```bash
cd bug-report-formatter
uvicorn main:app --port 8000
```

**Gör:** Öppna `http://localhost:8000` i webbläsaren.

**Gör:** Klistra in en riktig buggbeskrivning i textfältet:

```
login knappen funkar inte på mobil, testade iphone 13, chrome, 
klickar men inget händer, funkar på desktop
```

**Gör:** Klicka Formatera och visa resultatet för publiken.

**Säg:**
> "Det här byggdes utan att jag själv skrev en enda rad kod. Men jag styrde varje steg — problemet, planen, verifieringen. Det är vibe coding."

---

## Steg 6: Summera metodiken (1 min)

**Säg:**
> "Vad demonstrerade vi precis?"

**Peka på varje punkt:**

1. Vi började med ett **verkligt problem** — inte en teknisk spec
2. Vi **planerade** innan vi implementerade
3. Vi jobbade i **korta sessioner med ett fokuserat mål** — inte en lång session som driftar
4. AI:n implementerade i **isolerade roller** — builder, reviewer
5. **Kvalitetsgrindar** stoppade dålig kod innan nästa steg
6. **Memory och skills** laddades automatiskt — vi behövde inte orientera AI:n från scratch
7. Vi behandlade AI-output som en **overifierad build** — kontrollen är vår

**Säg:**
> "Det är skillnaden mellan att prompta och att jobba strukturerat med AI. En ger ett svar. Den andra ger ett system."

---

## Fallback om något går fel live

- **Claude svarar långsamt:** Förklara att det är normalt — AI:n tänker, inte hänger
- **Implementeringen tar för lång tid:** Hoppa till `cd bug-report-formatter` och visa det färdiga resultatet direkt
- **Appen startar inte:** Visa koden i `main.py` och förklara strukturen istället
- **Claude svarar inte:** Kontrollera att `claude` är inloggat — kör `claude --version` i en annan terminal

---

## Tidsplan

| Steg | Tid |
|------|-----|
| Problemet | 2 min |
| Presentera idén + memory/skills | 3 min |
| Planera | 3 min |
| Sessioner och context | 2 min |
| Implementera + kvalitetsgrindar | 4 min |
| Visa resultatet | 2 min |
| Summera | 1 min |
| **Totalt** | **17 min** |
