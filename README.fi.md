[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Čeština](README.cs.md) | [Dansk](README.da.md) | [Deutsch](README.de.md) | [Esperanto](README.eo.md) | [فارسی](README.fa.md) | [Suomi](README.fi.md) | [Français](README.fr.md) | [Ελληνικά](README.gr.md) | [Magyar](README.hu.md) | [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [മലയാളം](README.ml.md) | [Nederlands](README.nl.md) | [Norsk](README.no.md) | [Polski](README.pl.md) | [Português](README.ptbr.md) | [Română](README.ro.md) | [Türkçe](README.tr.md) | [Українська](README.ua.md) | [Tiếng Việt](README.vn.md)

# ☁️ Cloud-Windows — Ilmainen pilvi-Windows-työpöytä

Muuta ilmainen GitHub Actions -Windows-virtuaalikone pilvityöpöydäksi, jota voit käyttää selaimestasi. Avaa verkkosivu ja sinulla on Windows-tietokone — sammuta se, kun olet valmis. Täysin ilmainen.

## ✨ Ominaisuudet

- 🖥️ Kokonainen Windows-työpöytä suoraan selaimessasi (noVNC-verkkosovellus)
- 📐 **Automaattinen tarkkuus**: sivun avaamisen jälkeen työpöydän tarkkuus mukautuu automaattisesti selainikkunasi kokoon — puhelimet ja tietokoneet saavat kumpikin sopivan sovituksen; se seuraa myös, kun muutat ikkunan kokoa
- 🌐 Pääsy Cloudflare Tunnel -yhteyden kautta — ei julkista IP-osoitetta, ei NAT-läpivientiä tarvita
- ⌨️ Sisäänrakennettu kiinalainen Sogou Pinyin -syöttötapa, kiinalainen syöttö toimii heti (`Win + Space` vaihtaa kiinan ja englannin välillä)
- 🖱️ Yhdistä puhelimesta, tabletilta tai tietokoneelta
- ⏱️ Jokainen ajo kestää jopa ~6 tuntia, ja voit peruuttaa milloin tahansa
- 📦 **RustDesk-versio**: tarjolla on myös RustDesk-työnkulku, joka lataa automaattisesti uusimman RustDesk-asennusohjelman työpöydälle

## 🚀 Käyttö (toimii heti forkkauksen jälkeen)

### Vaihe 1: Forkkaa tämä projekti

Napsauta sivun oikeassa yläkulmassa olevaa **Fork**-painiketta kopioidaksesi projektin omaan GitHub-tiliisi. Forkkauksen jälkeen päädyt repositorioon `your-username/Cloud-Windows`.

> 💡 Miksi forkata? GitHub Actions voi toimia vain oman tilisi alla olevissa repositorioissa — forkkaus antaa sinulle suoritusluvan.

### Vaihe 2: Käynnistä pilvityöpöytä

1. Mene forkkaamasi repositorion sivulle ja napsauta ylhäällä **Actions**-välilehteä
2. Valitse vasemmalta työnkulku (valitse yksi):
   - **Windows Cloud Desktop**: vakio-pilvityöpöytä
   - **Windows Cloud Desktop + RustDesk**: vakioversio sekä uusimman RustDesk-asennusohjelman automaattinen lataus työpöydälle (versiota ei ole kovakoodattu — hakee aina uusimman virallisen julkaisun); kaksoisnapsauta asentaaksesi, kun tarvitset etäohjausta
3. Napsauta oikealla **Run workflow** -painiketta — avautuu valintaikkuna, jossa on kolme syöttökenttää:

| Parametri | Kuvaus |
|------|------|
| VNC-salasana | Salasana, jonka annat yhdistäessäsi työpöytään — vain kirjaimia ja numeroita, enintään 8 merkkiä (esim. `abc12345`). **Kirjoita se muistiin** |
| Ajoaika | Kuinka monta minuuttia tämä pilvityöpöytäistunto pysyy käynnissä. Oletus 300 (5 tuntia), maksimi 350 |
| Tarkkuus | Työpöydän alkutarkkuus, oletus 1920x1080; heti kun avaat sivun selaimessasi, se mukautuu automaattisesti ikkunasi kokoon |

4. Vahvista napsauttamalla vihreää **Run workflow**-painiketta — pilvityöpöytä alkaa käynnistyä

### Vaihe 3: Hae käyttöosoite

1. Napsauta Actions-sivulla äsken aloittamaasi ajoa (ylimmäinen — keltainen piste tarkoittaa, että se on käynnissä)
2. Odota noin 3–5 minuuttia, kun virtuaalikone asentaa ohjelmistoja ja muodostaa tunnelin
3. Napsauta vaihetta **启动服务并建立隧道**, laajenna lokit ja vieritä alas löytääksesi tällaisen osoitteen:

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. Kopioi osoite ja avaa se selaimessasi (puhelimesi sisäänrakennettu selain toimii hyvin)

### Vaihe 4: Yhdistä työpöytään

1. Napsauta avautuvalla noVNC-sivulla **Connect**
2. Anna vaiheessa 2 asettamasi VNC-salasana
3. Olet sisällä — nauti Windows-työpöydästäsi 🎉
4. Työpöydän tarkkuus mukautuu automaattisesti selainikkunaasi noin 10 sekunnin kuluessa sivun avaamisesta; ikkunan koon muuttaminen laukaisee automaattisen uudelleensovituksen (valitaan GPU:si tukemista tarkkuuksista)

> ⌨️ Vaihda syöttötapaa Sogou Pinyinin ja englantilaisen näppäimistön välillä painamalla **Win + Space**.

### Vaihe 5: Sammuta se, kun olet valmis

- Palaa Actions-sivulle, avaa ajo ja napsauta oikeassa yläkulmassa **Cancel run** — virtuaalikone tuhotaan ja tunneli kuolee
- Se myös päättyy automaattisesti, kun asetettu kesto umpeutuu, joten sinun ei tarvitse huolehtia siitä, että se jäisi päälle ikuisiksi ajoiksi

## ⚠️ Huomioitavaa

- **Osoite vaihtuu jokaisella ajolla**: vanha osoite lakkaa toimimasta heti, kun edellinen ajo päättyy, joten käytä aina uusimman ajon lokeissa olevaa osoitetta
- **Mitään ei tallenneta**: kun virtuaalikone tuhotaan, työpöydän tiedostot, lataukset ja kirjautumistilat pyyhitään kaikki — siirrä tärkeät tiedostot pois ajoissa
- **Salasanasäännöt**: vain kirjaimia ja numeroita, enintään 8 merkkiä — pidemmät salasanat tai erikoismerkkejä sisältävät salasanat eivät välttämättä yhdistä (virheenä `Authentication failed`)
- **Älä napsauta Re-run**: aloita uusi työpöytä napsauttamalla **Run workflow** — Re-run toistaa vanhaa koodia
- **Hidas/nykinen yhteys**: tunneli kulkee Cloudflaren kautta; nopeudet Manner-Kiinasta riippuvat verkostasi, mutta se on käyttökelpoinen
- **Sivu ei aukea**: tarkista ensin, että ajo on vielä käynnissä (keltainen piste) — jos se on peruutettu tai päättynyt, osoite on kuollut

## ❓ UKK

| Oire | Syy / korjaus |
|------|-----------|
| `loopback connections are not enabled` | Vanhan version bugi — aloita uusi ajo uusimmalla koodilla Run workflow -painikkeella |
| `Server is not configured properly` | Vanhan version bugi — aloita uusi ajo uusimmalla koodilla Run workflow -painikkeella |
| `Authentication failed` | Väärä VNC-salasana, tai salasana on yli 8 merkkiä / sisältää erikoismerkkejä |
| 502 / 1033 sivulla | Tunneli ei ole vielä ylhäällä tai on kaatunut — odota muutama minuutti tai aja uudelleen |
| Tarkkuus ei muuttunut automaattisesti | Odota ~10 sekuntia; varmista, että selainikkunan koko todella muuttui; GPU ei tue joitakin epästandardeja tarkkuuksia, jolloin valitaan lähin vaihtoehto |

## 🛠️ Haluatko säätää itse?

Työnkulkutiedostot ovat kohdassa `.github/workflows/` (`windows-vnc.yml` vakioversiolle, `windows-vnc-rustdesk.yml` RustDesk-versiolle) — voit muokata niitä suoraan GitHubin verkkosivulla; muutokset astuvat voimaan commitin jälkeen.
