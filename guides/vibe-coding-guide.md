# Vibe Coding Guide
## Sätt upp ett bra AI-arbetsflöde på vilket projekt som helst

---

## Välj ditt spår

**Befintligt repo** → Tänk som en testare. Vad är okänt? Vad kan skada dig?

**Nytt projekt** → Tänk som en arkitekt. Bygg så att AI:n alltid har rätt kontext och rätt begränsningar.

---

## Spår 1: Befintligt repo

### 1. Isolera först

Kör AI:n isolerat från resten av systemet. Den ska bara nå projektmappen — inte `~/.ssh`, `~/.env`, `~/.aws` eller andra personliga filer.

```bash
cd ditt-projekt/
claude   # starta inne i projektet
```

Om du kör autonoma loopar: använd Docker eller en devcontainer.

### 2. Inventera

Låt AI:n läsa projektet och skapa ett utkast till `CLAUDE.md`:

```
Läs igenom koden och skriv en CLAUDE.md som förklarar:
- Vad projektet gör
- Hur det byggs
- Hur det testas
- Vilka kommandon som används
Var specifik.
```

Granska och justera utkastet. `CLAUDE.md` laddas automatiskt i varje ny session.

### 3. Lägg till regler

Lägg begränsningar direkt i `CLAUDE.md`:

```markdown
## Regler
- Planera alltid innan du implementerar
- Kör alltid tester innan du committar
- Committa aldrig direkt till main
- Fråga innan du ändrar något utanför projektmappen
- Kör aldrig deployer utan explicit instruktion
```

Anpassa efter vad som är farligt i ditt projekt.

### 4. Lägg till skills

Skills är återanvändbara arbetsflöden. Skapa dem i `~/.claude/skills/` som `.md`-filer.

Börja med det du gör oftast. En skill för testgranskning:

```markdown
---
name: test-review
description: "Use when reviewing a test case"
---

Granska det här testet:
- Är setup tydlig?
- Är hårdvarutillståndet kontrollerat?
- Fångas loggar?
- Är cleanup inkluderat?
- Kan testet misslyckas av miljöskäl?
- Är det produkt-, test-, rigg- eller infrastruktur-issue?
```

### 5. Lägg till hooks sist

Hooks kör automatiskt vid händelser. Lägg till dem när du vet exakt vad du vill automatisera — inte innan.

---

## Spår 2: Nytt projekt

### 1. Skapa sandbox

```bash
mkdir mitt-projekt && cd mitt-projekt
git init
```

Sätt upp isolering innan du skriver en enda rad kod. Docker eller devcontainer om du kör autonoma agenter.

### 2. Skapa CLAUDE.md

Skriv den innan AI:n börjar arbeta:

```markdown
# mitt-projekt

## Vad det är
[Beskriv problemet — ett konkret problem, inte en teknisk spec]

## Hur det byggs
[Kommando]

## Hur det testas
[Kommando]

## Regler
- Planera innan du implementerar
- Kör tester innan du committar
- Committa aldrig direkt till main
- Fråga innan du ändrar något utanför projektmappen
```

### 3. Skapa teststrategi

Bestäm vad "klart" betyder innan AI:n börjar:

```markdown
## Definition of done
- Appen startar utan fel
- Testerna går igenom
- Lintaren är nöjd
- Manuell genomgång av huvudflödet
```

### 4. Skapa scripts

Lägg grundläggande scripts på plats:

```
scripts/
  test.sh    # kör tester
  lint.sh    # kör linting
  build.sh   # bygger projektet
```

AI:n ska använda dessa — inte hitta på egna kommandon.

### 5. Skapa skills

Skriv skills för de arbetsflöden du vet att du kommer upprepa. Domänspecifika skills är mer värda än generiska.

### 6. Bygg sedan kod

Nu är du redo. Starta Claude Code och presentera problemet i vanligt språk:

```bash
claude
```

```
Jag vill bygga [problemet, inte lösningen].
Kan du hjälpa mig planera det?
```

Låt AI:n planera. Granska planen. Implementera sedan — ett steg i taget.

---

## Arbetsflödet i varje session

```
1. Ett fokuserat mål — inte "gör allt"
2. Planera → implementera → verifiera → granska
3. Stäng sessionen när målet är klart
4. Nästa session börjar med nästa mål
```

Långa sessioner driftar. Korta sessioner med tydliga mål ger stabila resultat.

---

## Prompta vs strukturera

Använd plain prompting för enkla saker:
- Förklara det här felet
- Skriv om den här texten
- Ge mig fem testidéer

Använd strukturerade workflows för allt du skulle skämmas för att leverera fel:

```
Prompting  = brainstorma
Skills     = repeterbar metod
Hooks      = automatiska kontroller
Memory     = stabil sanning
Agenter    = avgränsade specialister
CI         = bevis
```

---

## Säkerhet: rätt frågor

En agent med shell-access kan påverkas av prompt injection — ett elakt PR-kommentar, en README, en PDF kan styra agenten om den behandlar all text som instruktioner.

Fråga dig efter varje körning:

```
Vad läste den?
Vad ändrade den?
Vilket kommando körde den?
Vilken behörighet använde den?
Vilket bevis finns på resultatet?
Kunde fientlig input ha påverkat den?
Kan jag stoppa den om något går fel?
```

Behandla AI-output som en overifierad build — användbar, men inte betrodd förrän kontrollerad.

---

## Snabbreferens

| Situation | Gör |
|-----------|-----|
| Ny session startar | Kontrollera att `CLAUDE.md` är uppdaterad |
| Innan implementering | Kräv en plan — inte direkt kod |
| Efter implementering | Kör tester, linta, granska diff |
| Sessionen driftar | Stäng. Starta ny session med ett mål. |
| AI:n gör något oväntat | Stoppa. Granska. Förstå vad som hände. |
| Känsliga filer i närheten | Kontrollera att AI:n inte når dem |
