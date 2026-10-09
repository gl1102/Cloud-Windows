[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Čeština](README.cs.md) | [Dansk](README.da.md) | [Deutsch](README.de.md) | [Esperanto](README.eo.md) | [فارسی](README.fa.md) | [Suomi](README.fi.md) | [Français](README.fr.md) | [Ελληνικά](README.gr.md) | [Magyar](README.hu.md) | [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [മലയാളം](README.ml.md) | [Nederlands](README.nl.md) | [Norsk](README.no.md) | [Polski](README.pl.md) | [Português](README.ptbr.md) | [Română](README.ro.md) | [Türkçe](README.tr.md) | [Українська](README.ua.md) | [Tiếng Việt](README.vn.md)

# ☁️ Cloud-Windows — Gratis cloud-Windows-skrivebord

Gør en gratis GitHub Actions Windows-VM til et cloud-skrivebord, du kan tilgå fra din browser. Åbn en webside, og du har en Windows-pc — luk den ned, når du er færdig. Helt gratis.

## ✨ Funktioner

- 🖥️ Et fuldt Windows-skrivebord, direkte i din browser (noVNC-webklient)
- 📐 **Automatisk opløsning**: Når du har åbnet siden, tilpasses skrivebordets opløsning automatisk til størrelsen på dit browservindue — telefoner og pc'er får hver især den rigtige tilpasning; den følger også med, når du ændrer vinduets størrelse
- 🌐 Adgang via Cloudflare Tunnel — ingen offentlig IP, ingen NAT-traversal nødvendig
- ⌨️ Indbygget Sogou Pinyin-tastaturmetode, kinesisk input virker med det samme (tryk på `Win + Space` for at skifte mellem kinesisk og engelsk)
- 🖱️ Forbind fra din telefon, tablet eller computer
- ⏱️ Hver kørsel varer op til ~6 timer, og du kan annullere når som helst
- 📦 **RustDesk-udgave**: der er også en RustDesk-workflow, der automatisk downloader den nyeste RustDesk-installer til Skrivebordet

## 🚀 Brug (virker lige efter forking)

### Trin 1: Fork dette projekt

Klik på knappen **Fork** øverst til højre på denne side for at kopiere projektet til din egen GitHub-konto. Når du har forket, lander du i depotet `your-username/Cloud-Windows`.

> 💡 Hvorfor forke? GitHub Actions kan kun køre i depoter under din egen konto — forking giver dig tilladelse til at køre det.

### Trin 2: Start cloud-skrivebordet

1. Gå til din forkede repos side, og klik på fanen **Actions** øverst
2. Vælg en workflow til venstre (vælg én):
   - **Windows Cloud Desktop**: standard-cloud-skrivebordet
   - **Windows Cloud Desktop + RustDesk**: standardudgaven plus automatisk download af den nyeste RustDesk-installer til Skrivebordet (versionen er ikke hardkodet — henter altid den nyeste officielle udgivelse); dobbeltklik for at installere, når du har brug for fjernstyring
3. Klik på knappen **Run workflow** til højre — en dialog med tre inputfelter dukker op:

| Parameter | Beskrivelse |
|------|------|
| VNC-adgangskode | Adgangskoden, du indtaster, når du opretter forbindelse til skrivebordet — kun bogstaver og tal, op til 8 tegn (f.eks. `abc12345`). **Skriv den ned** |
| Køretid | Hvor mange minutter denne cloud-skrivebordssession forbliver aktiv. Standard 300 (5 timer), maks. 350 |
| Opløsning | Den indledende skrivebordsopløsning, standard 1920x1080; når du åbner siden i din browser, tilpasses den automatisk til dit vindues størrelse |

4. Klik på den grønne **Run workflow** for at bekræfte — cloud-skrivebordet begynder at starte op

### Trin 3: Få adgangs-URL'en

1. På Actions-siden skal du klikke ind i den kørsel, du lige har startet (den øverste — en gul prik betyder, at den kører)
2. Vent ca. 3–5 minutter, mens VM'en installerer software og sætter tunnelen op
3. Klik på trinnet **启动服务并建立隧道**, udvid loggene, og rul ned for at finde en URL som denne:

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. Kopiér URL'en, og åbn den i din browser (din telefons indbyggede browser fungerer fint)

### Trin 4: Forbind til skrivebordet

1. På den noVNC-side, der åbnes, skal du klikke på **Connect**
2. Indtast den VNC-adgangskode, du angav i trin 2
3. Du er inde — nyd dit Windows-skrivebord 🎉
4. Skrivebordets opløsning tilpasses automatisk til dit browservindue inden for ca. 10 sekunder efter åbning af siden; ændring af vinduets størrelse udløser en automatisk tilpasning (valgt blandt de opløsninger, din GPU understøtter)

> ⌨️ Tryk på **Win + Space** for at skifte inputmetode mellem Sogou Pinyin og det engelske tastatur.

### Trin 5: Luk det ned, når du er færdig

- Gå tilbage til Actions-siden, åbn kørslen, og klik på **Cancel run** øverst til højre — VM'en ødelægges, og tunnelen dør
- Den slutter også automatisk, når den indstillede varighed er gået, så du behøver ikke bekymre dig om, at den kører for evigt

## ⚠️ Bemærkninger

- **URL'en ændres ved hver kørsel**: den gamle URL holder op med at virke, så snart den forrige kørsel slutter, så brug altid URL'en fra den seneste kørsels logge
- **Intet gemmes**: når VM'en er ødelagt, slettes filer, downloads og login-tilstande på skrivebordet — flyt vigtige filer ud i tide
- **Adgangskoderegler**: kun bogstaver og tal, op til 8 tegn — længere adgangskoder eller adgangskoder med specialtegn kan muligvis ikke oprette forbindelse (med `Authentication failed`)
- **Klik ikke på Re-run**: for at starte et nyt skrivebord skal du klikke på **Run workflow** — Re-run afspiller gammel kode
- **Langsom/hakkende forbindelse**: tunnelen går gennem Cloudflare; hastigheder fra det kinesiske fastland afhænger af dit netværk, men den er brugbar
- **Siden vil ikke åbne**: tjek først, at kørslen stadig er i gang (gul prik) — hvis den er annulleret eller færdig, er URL'en død

## ❓ Ofte stillede spørgsmål

| Symptom | Årsag / løsning |
|------|-----------|
| `loopback connections are not enabled` | Fejl i gammel version — start en ny kørsel med den nyeste kode via Run workflow |
| `Server is not configured properly` | Fejl i gammel version — start en ny kørsel med den nyeste kode via Run workflow |
| `Authentication failed` | Forkert VNC-adgangskode, eller adgangskoden er over 8 tegn / indeholder specialtegn |
| 502 / 1033 på siden | Tunnelen er ikke oppe endnu eller er faldet — vent et par minutter, eller kør igen |
| Opløsningen ændrede sig ikke automatisk | Vent ~10 sekunder; sørg for, at browservinduets størrelse faktisk ændrede sig; nogle ikke-standard opløsninger understøttes ikke af GPU'en, og den nærmeste vælges i stedet |

## 🛠️ Vil du selv justere det?

Workflow-filerne ligger under `.github/workflows/` (`windows-vnc.yml` for standardudgaven, `windows-vnc-rustdesk.yml` for RustDesk-udgaven) — du kan redigere dem direkte på GitHubs hjemmeside; ændringer træder i kraft, når du committer.
