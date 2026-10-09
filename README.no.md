[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Čeština](README.cs.md) | [Dansk](README.da.md) | [Deutsch](README.de.md) | [Esperanto](README.eo.md) | [فارسی](README.fa.md) | [Suomi](README.fi.md) | [Français](README.fr.md) | [Ελληνικά](README.gr.md) | [Magyar](README.hu.md) | [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [മലയാളം](README.ml.md) | [Nederlands](README.nl.md) | [Norsk](README.no.md) | [Polski](README.pl.md) | [Português](README.ptbr.md) | [Română](README.ro.md) | [Türkçe](README.tr.md) | [Українська](README.ua.md) | [Tiếng Việt](README.vn.md)

# ☁️ Cloud-Windows — Gratis Windows-skrivebord i skyen

Gjør en gratis GitHub Actions-Windows-VM om til et skrivebord i skyen du kan bruke fra nettleseren. Åpne en nettside, så har du en Windows-PC — slå den av når du er ferdig. Helt gratis.

## ✨ Funksjoner

- 🖥️ Et fullverdig Windows-skrivebord, rett i nettleseren (noVNC-nettklient)
- 📐 **Automatisk oppløsning**: etter at du har åpnet siden, tilpasses skrivebordsoppløsningen automatisk nettleservinduets størrelse — telefoner og PC-er får hver sin optimale visning; den følger med når du endrer vinduets størrelse også
- 🌐 Tilgang via Cloudflare Tunnel — ingen offentlig IP, ingen NAT-traversering nødvendig
- ⌨️ Innebygd Sogou Pinyin-IME, kinesisk inndata fungerer med en gang (trykk `Win + Space` for å bytte mellom kinesisk og engelsk)
- 🖱️ Koble til fra telefonen, nettbrettet eller datamaskinen
- ⏱️ Hver kjøring varer opptil ~6 timer, og du kan avbryte når som helst
- 📦 **RustDesk-utgave**: det finnes også en RustDesk-arbeidsflyt som automatisk laster ned det nyeste RustDesk-installasjonsprogrammet til skrivebordet (installer selv, eller bruk den portable versjonen for fjernkontroll)

## 🚀 Bruk (fungerer rett etter forking)

### Trinn 1: Fork dette prosjektet

Klikk på **Fork**-knappen øverst til høyre på denne siden for å kopiere prosjektet til din egen GitHub-konto (forken kopierer `main`-grenen — ikke velg `test`-grenen, den er kun til testing). Når du har forket, lander du i depotet `your-username/Cloud-Windows`.

> 💡 Hvorfor forke? GitHub Actions kan bare kjøre i depoter under din egen konto — forking gir deg tillatelse til å kjøre det.

### Trinn 2: Start skrivebordet i skyen

1. Gå til siden for det forkede depotet og klikk på **Actions**-fanen øverst
2. Velg en arbeidsflyt til venstre (velg én):
   - **Windows Cloud Desktop**: det vanlige skrivebordet i skyen
   - **Windows Cloud Desktop + RustDesk**: standardutgaven pluss automatisk nedlasting av det nyeste RustDesk-installasjonsprogrammet (`rustdesk-x.x.x-x86_64.exe`) til skrivebordet (versjonen er ikke hardkodet — henter alltid den nyeste offisielle utgaven); for fjernkontroll med RustDesk: dobbeltklikk for å installere, eller kjør den portable RustDesk-versjonen direkte uten installasjon
3. Klikk på **Run workflow**-knappen til høyre — en dialog med tre inndatafelt dukker opp:

| Parameter | Beskrivelse |
|------|------|
| VNC password | Passordet du skriver inn når du kobler til skrivebordet — kun bokstaver og tall, maks 8 tegn (f.eks. `abc12345`). **Skriv det ned** |
| Run duration | Hvor mange minutter denne skrivebordsøkten i skyen holder seg aktiv. Standard 300 (5 timer), maks 350 |
| Resolution | Den innledende skrivebordsoppløsningen, standard 1920x1080; når du åpner siden i nettleseren, tilpasses den automatisk til vindusstørrelsen din |

4. Klikk på den grønne **Run workflow**-knappen for å bekrefte — skrivebordet i skyen begynner å starte opp

### Trinn 3: Hent tilgangs-URL-en

1. På Actions-siden klikker du inn i kjøringen du nettopp startet (den øverste — en gul prikk betyr at den kjører)
2. Vent omtrent 3–5 minutter mens VM-en installerer programvare og setter opp tunnelen
3. Klikk på steget **启动服务并建立隧道**, utvid loggene, og bla nedover for å finne en URL som denne:

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. Kopier URL-en og åpne den i nettleseren din (telefonens innebygde nettleser fungerer fint)

### Trinn 4: Koble til skrivebordet

1. På noVNC-siden som åpnes, klikker du **Connect**
2. Skriv inn VNC-passordet du satte i trinn 2
3. Nå er du inne — kos deg med Windows-skrivebordet 🎉
4. Skrivebordsoppløsningen tilpasser seg automatisk til nettleservinduet ditt innen omtrent 10 sekunder etter at du åpner siden; endring av vinduets størrelse utløser automatisk ny tilpasning (valgt blant oppløsningene GPU-en din støtter)

> ⌨️ Trykk **Win + Space** for å bytte inndatametode mellom Sogou Pinyin og det engelske tastaturet.

### Trinn 5: Slå det av når du er ferdig

- Gå tilbake til Actions-siden, åpne kjøringen, og klikk **Cancel run** øverst til høyre — VM-en ødelegges og tunnelen dør
- Den avsluttes også automatisk når den angitte varigheten er over, så du trenger ikke bekymre deg for at den kjører for alltid

## ⚠️ Merknader

- **URL-en endres ved hver kjøring**: den gamle URL-en slutter å virke så snart forrige kjøring er avsluttet, så bruk alltid URL-en fra den nyeste kjøringens logger
- **Ingenting lagres**: når VM-en ødelegges, slettes filer, nedlastinger og påloggingsstatuser på skrivebordet — flytt viktige filer ut i tide
- **Passordregler**: kun bokstaver og tall, maks 8 tegn — lengre passord eller passord med spesialtegn kan mislykkes ved tilkobling (med `Authentication failed`)
- **Ikke klikk Re-run**: for å starte et nytt skrivebord, klikk **Run workflow** — Re-run spiller av gammel kode
- **Treg/hakkete tilkobling**: tunnelen går gjennom Cloudflare; hastigheter fra Fastlands-Kina avhenger av nettverket ditt, men det er brukbart
- **Siden åpnes ikke**: sjekk først at kjøringen fortsatt pågår (gul prikk) — hvis den er avbrutt eller ferdig, er URL-en død

## ❓ FAQ

| Symptom | Årsak / Løsning |
|------|-----------|
| `loopback connections are not enabled` | Feil i gammel versjon — start en ny kjøring med den nyeste koden via Run workflow |
| `Server is not configured properly` | Feil i gammel versjon — start en ny kjøring med den nyeste koden via Run workflow |
| `Authentication failed` | Feil VNC-passord, eller passordet er over 8 tegn / inneholder spesialtegn |
| 502 / 1033 på siden | Tunnelen er ikke oppe ennå eller har falt ned — vent noen minutter eller kjør på nytt |
| Oppløsningen endret seg ikke automatisk | Vent ~10 sekunder; sørg for at nettleservinduet faktisk endret størrelse; noen ikke-standardoppløsninger støttes ikke av GPU-en, og den nærmeste velges i stedet |

## 🛠️ Vil du tilpasse det selv?

Arbeidsflytfilene ligger under `.github/workflows/` (`windows-vnc.yml` for standardutgaven, `windows-vnc-rustdesk.yml` for RustDesk-utgaven) — du kan redigere dem direkte på GitHub-nettstedet; endringer trer i kraft etter at du committer.
