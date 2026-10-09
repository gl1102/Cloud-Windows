[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Čeština](README.cs.md) | [Dansk](README.da.md) | [Deutsch](README.de.md) | [Esperanto](README.eo.md) | [فارسی](README.fa.md) | [Suomi](README.fi.md) | [Français](README.fr.md) | [Ελληνικά](README.gr.md) | [Magyar](README.hu.md) | [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [മലയാളം](README.ml.md) | [Nederlands](README.nl.md) | [Norsk](README.no.md) | [Polski](README.pl.md) | [Português](README.ptbr.md) | [Română](README.ro.md) | [Türkçe](README.tr.md) | [Українська](README.ua.md) | [Tiếng Việt](README.vn.md)

# ☁️ Cloud-Windows — Gratis cloud-Windows-bureaublad

Verander een gratis GitHub Actions Windows-VM in een cloudbureaublad dat je vanuit je browser kunt gebruiken. Open een webpagina en je hebt een Windows-pc — zet hem uit als je klaar bent. Helemaal gratis.

## ✨ Functies

- 🖥️ Een volledig Windows-bureaublad, gewoon in je browser (noVNC-webclient)
- 📐 **Automatische resolutie**: nadat je de pagina hebt geopend, past de bureaubladresolutie zich automatisch aan de grootte van je browservenster aan — telefoons en pc's krijgen elk de juiste weergave; het volgt ook als je het venster vergroot of verkleint
- 🌐 Toegang via Cloudflare Tunnel — geen openbaar IP nodig, geen NAT-traversal nodig
- ⌨️ Ingebouwde Sogou Pinyin-invoermethode, Chinese invoer werkt direct (`Win + Space` om te schakelen tussen Chinees en Engels)
- 🖱️ Verbind vanaf je telefoon, tablet of computer
- ⏱️ Elke sessie duurt tot ~6 uur, en je kunt hem op elk moment annuleren
- 📦 **RustDesk-editie**: er is ook een RustDesk-workflow die automatisch de nieuwste RustDesk naar de D-schijf downloadt en stil installeert naar `D:\RustDesk`

## 🚀 Gebruik (werkt direct na het forken)

### Stap 1: Fork dit project

Klik op de knop **Fork** rechtsboven op deze pagina om het project naar je eigen GitHub-account te kopiëren. Na het forken kom je in de repository `your-username/Cloud-Windows`.

> 💡 Waarom forken? GitHub Actions kan alleen draaien in repositories onder je eigen account — forken geeft je toestemming om het uit te voeren.

### Stap 2: Start het cloudbureaublad

1. Ga naar de pagina van je geforkte repo en klik bovenaan op het tabblad **Actions**
2. Kies links een workflow (kies er één):
   - **Windows Cloud Desktop**: het standaard cloudbureaublad
   - **Windows Cloud Desktop + RustDesk**: standaardeditie plus automatische download van de nieuwste RustDesk naar de D-schijf met stille installatie naar `D:\RustDesk` (versie niet hardcoded — haalt altijd de nieuwste officiële release op)
3. Klik rechts op de knop **Run workflow** — er verschijnt een dialoogvenster met drie invoervelden:

| Parameter | Beschrijving |
|------|------|
| VNC-wachtwoord | Het wachtwoord dat je invoert bij het verbinden met het bureaublad — alleen letters en cijfers, maximaal 8 tekens (bijv. `abc12345`). **Schrijf het op** |
| Sessieduur | Hoeveel minuten deze cloudbureaubladsessie actief blijft. Standaard 300 (5 uur), maximaal 350 |
| Resolutie | De initiële bureaubladresolutie, standaard 1920x1080; zodra je de pagina in je browser opent, past deze zich automatisch aan je venstergrootte aan |

4. Klik op de groene knop **Run workflow** om te bevestigen — het cloudbureaublad start op

### Stap 3: Haal de toegangs-URL op

1. Klik op de Actions-pagina op de sessie die je zojuist hebt gestart (de bovenste — een gele stip betekent dat hij draait)
2. Wacht ongeveer 3–5 minuten tot de VM de software heeft geïnstalleerd en de tunnel heeft opgezet
3. Klik op de stap **启动服务并建立隧道**, vouw de logs uit en scrol naar beneden om een URL zoals deze te vinden:

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. Kopieer de URL en open hem in je browser (de ingebouwde browser van je telefoon werkt prima)

### Stap 4: Verbind met het bureaublad

1. Klik op de noVNC-pagina die opent op **Connect**
2. Voer het VNC-wachtwoord in dat je in stap 2 hebt ingesteld
3. Je bent binnen — veel plezier met je Windows-bureaublad 🎉
4. De bureaubladresolutie past zich binnen ongeveer 10 seconden na het openen van de pagina automatisch aan je browservenster aan; het vergroten of verkleinen van het venster activeert een automatische aanpassing (gekozen uit de resoluties die je GPU ondersteunt)

> ⌨️ Druk op **Win + Space** om de invoermethode te schakelen tussen Sogou Pinyin en het Engelse toetsenbord.

### Stap 5: Zet hem uit als je klaar bent

- Ga terug naar de Actions-pagina, open de sessie en klik rechtsboven op **Cancel run** — de VM wordt vernietigd en de tunnel valt weg
- Hij stopt ook automatisch zodra de ingestelde duur is verstreken, dus je hoeft je geen zorgen te maken dat hij voor altijd blijft draaien

## ⚠️ Opmerkingen

- **De URL verandert elke sessie**: de oude URL stopt met werken zodra de vorige sessie is beëindigd, dus gebruik altijd de URL uit de logs van de nieuwste sessie
- **Er wordt niets bewaard**: zodra de VM is vernietigd, worden bestanden, downloads en aanmeldingsstatussen op het bureaublad allemaal gewist — haal belangrijke bestanden op tijd weg
- **Wachtwoordregels**: alleen letters en cijfers, maximaal 8 tekens — langere wachtwoorden of wachtwoorden met speciale tekens kunnen mislukken bij het verbinden (met `Authentication failed`)
- **Klik niet op Re-run**: om een nieuw bureaublad te starten, klik op **Run workflow** — Re-run speelt oude code opnieuw af
- **Trage/laggende verbinding**: de tunnel loopt via Cloudflare; snelheden vanuit het vasteland van China hangen af van je netwerk, maar het is bruikbaar
- **Pagina opent niet**: controleer eerst of de sessie nog loopt (gele stip) — als hij is geannuleerd of beëindigd, is de URL dood

## ❓ Veelgestelde vragen

| Symptoom | Oorzaak / Oplossing |
|------|-----------|
| `loopback connections are not enabled` | Bug in oude versie — start een nieuwe sessie met de nieuwste code via Run workflow |
| `Server is not configured properly` | Bug in oude versie — start een nieuwe sessie met de nieuwste code via Run workflow |
| `Authentication failed` | Verkeerd VNC-wachtwoord, of het wachtwoord is langer dan 8 tekens / bevat speciale tekens |
| 502 / 1033 in de pagina | Tunnel staat nog niet op of is weggevallen — wacht een paar minuten of draai opnieuw |
| Resolutie veranderde niet automatisch | Wacht ~10 seconden; zorg dat de grootte van het browservenster echt is veranderd; sommige niet-standaardresoluties worden niet ondersteund door de GPU en de dichtstbijzijnde wordt gekozen |

## 🛠️ Wil je het zelf aanpassen?

De workflowbestanden staan onder `.github/workflows/` (`windows-vnc.yml` voor de standaardeditie, `windows-vnc-rustdesk.yml` voor de RustDesk-editie) — je kunt ze direct op de GitHub-website bewerken; wijzigingen zijn van kracht na een commit.
