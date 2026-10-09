[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Čeština](README.cs.md) | [Dansk](README.da.md) | [Deutsch](README.de.md) | [Esperanto](README.eo.md) | [فارسی](README.fa.md) | [Suomi](README.fi.md) | [Français](README.fr.md) | [Ελληνικά](README.gr.md) | [Magyar](README.hu.md) | [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [മലയാളം](README.ml.md) | [Nederlands](README.nl.md) | [Norsk](README.no.md) | [Polski](README.pl.md) | [Português](README.ptbr.md) | [Română](README.ro.md) | [Türkçe](README.tr.md) | [Українська](README.ua.md) | [Tiếng Việt](README.vn.md)

# ☁️ Cloud-Windows — Ingyenes felhő Windows asztal

Alakíts át egy ingyenes GitHub Actions Windows virtuális gépet böngészőből elérhető felhő asztallá. Nyiss meg egy weboldalt, és máris van egy Windows PC-d — ha végeztél, kapcsold ki. Teljesen ingyenes.

## ✨ Funkciók

- 🖥️ Teljes Windows asztal, közvetlenül a böngésződben (noVNC web kliens)
- 📐 **Automatikus felbontás**: az oldal megnyitása után az asztal felbontása automatikusan igazodik a böngészőablak méretéhez — telefonon és PC-n egyaránt a megfelelő illeszkedés; az ablak átméretezését is követi
- 🌐 Hozzáférés Cloudflare alagúton keresztül — nincs szükség nyilvános IP-re, sem NAT-átjárásra
- ⌨️ Beépített Sogou Pinyin beviteli mód, a kínai bevitel azonnal működik (nyomd meg a `Win + Space` billentyűt a kínai és az angol közötti váltáshoz)
- 🖱️ Csatlakozz telefonról, tabletről vagy számítógépről
- ⏱️ Minden futás legfeljebb ~6 óráig tart, és bármikor megszakíthatod
- 📦 **RustDesk kiadás**: van egy RustDesk munkafolyamat is, amely automatikusan letölti a legfrissebb RustDesk telepítőt az Asztalra

## 🚀 Használat (fork után azonnal működik)

### 1. lépés: Forkold ezt a projektet

Kattints a **Fork** gombra az oldal jobb felső sarkában, hogy a projektet a saját GitHub-fiókodba másold. A fork után a `your-username/Cloud-Windows` tárolóba jutsz.

> 💡 Miért fork? A GitHub Actions csak a saját fiókod alatti tárolókban futhat — a fork megadja a futtatáshoz szükséges jogosultságot.

### 2. lépés: Indítsd el a felhő asztalt

1. Menj a forkolt tároló oldalára, és kattints felül az **Actions** fülre
2. Válassz egy munkafolyamatot bal oldalt (válassz egyet):
   - **Windows Cloud Desktop**: a normál felhő asztal
   - **Windows Cloud Desktop + RustDesk**: normál kiadás, plusz a legfrissebb RustDesk telepítő automatikus letöltése az Asztalra (a verzió nincs beégetve — mindig a legfrissebb hivatalos kiadást tölti le); távoli vezérléshez csak kattints duplán a telepítéshez
3. Kattints a jobb oldali **Run workflow** gombra — felugrik egy párbeszédablak három beviteli mezővel:

| Paraméter | Leírás |
|------|------|
| VNC jelszó | A jelszó, amelyet az asztalhoz való csatlakozáskor adsz meg — csak betűk és számok, legfeljebb 8 karakter (pl. `abc12345`). **Írd fel** |
| Futási idő | Hány percig marad életben ez a felhő asztal munkamenet. Alapértelmezett 300 (5 óra), maximum 350 |
| Felbontás | Az asztal kezdeti felbontása, alapértelmezett 1920x1080; miután megnyitottad az oldalt a böngésződben, automatikusan igazodik az ablak méretéhez |

4. Kattints a zöld **Run workflow** gombra a megerősítéshez — a felhő asztal elindul

### 3. lépés: Szerezd meg a hozzáférési URL-t

1. Az Actions oldalon kattints a most indított futásra (a legfelső — a sárga pont azt jelenti, hogy fut)
2. Várj kb. 3–5 percet, amíg a VM telepíti a szoftvereket és felépíti az alagutat
3. Kattints a **启动服务并建立隧道** lépésre, bontsd ki a naplókat, és görgess lefelé, amíg egy ilyen URL-t nem találsz:

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. Másold ki az URL-t, és nyisd meg a böngésződben (a telefonod beépített böngészője is tökéletesen megfelel)

### 4. lépés: Csatlakozz az asztalhoz

1. A megnyíló noVNC oldalon kattints a **Connect** gombra
2. Add meg a 2. lépésben beállított VNC jelszót
3. Bent vagy — élvezd a Windows asztalt 🎉
4. Az asztal felbontása az oldal megnyitása után kb. 10 másodpercen belül automatikusan igazodik a böngészőablakodhoz; az ablak átméretezése automatikus újbóli illeszkedést vált ki (a GPU által támogatott felbontások közül választva)

> ⌨️ Nyomd meg a **Win + Space** billentyűt a beviteli mód váltásához a Sogou Pinyin és az angol billentyűzet között.

### 5. lépés: Ha végeztél, kapcsold ki

- Menj vissza az Actions oldalra, nyisd meg a futást, és kattints jobb felül a **Cancel run** gombra — a VM megsemmisül, az alagút pedig megszűnik
- A beállított időtartam letelte után automatikusan véget ér, így nem kell aggódnod, hogy örökké futna

## ⚠️ Megjegyzések

- **Az URL minden futásnál változik**: a régi URL érvényét veszti, amint az előző futás véget ér, ezért mindig a legutóbbi futás naplóiból származó URL-t használd
- **Semmi sem mentődik**: ha a VM megsemmisül, az asztalon lévő fájlok, letöltések és bejelentkezési állapotok mind törlődnek — a fontos fájlokat időben mentsd ki
- **Jelszószabályok**: csak betűk és számok, legfeljebb 8 karakter — a hosszabb vagy speciális karaktereket tartalmazó jelszavakkal a csatlakozás meghiúsulhat (`Authentication failed`)
- **Ne kattints a Re-run gombra**: új asztal indításához kattints a **Run workflow** gombra — a Re-run a régi kódot futtatja újra
- **Lassú/akadozó kapcsolat**: az alagút a Cloudflare-en keresztül megy; a Kínából mért sebesség a hálózatodtól függ, de használható
- **Az oldal nem nyílik meg**: először ellenőrizd, hogy a futás még folyamatban van-e (sárga pont) — ha megszakították vagy befejeződött, az URL halott

## ❓ Gyakori kérdések

| Tünet | Ok / Megoldás |
|------|-----------|
| `loopback connections are not enabled` | Régi verziós hiba — indíts új futást a legfrissebb kóddal a Run workflow segítségével |
| `Server is not configured properly` | Régi verziós hiba — indíts új futást a legfrissebb kóddal a Run workflow segítségével |
| `Authentication failed` | Hibás VNC jelszó, vagy a jelszó 8 karakternél hosszabb / speciális karaktereket tartalmaz |
| 502 / 1033 az oldalon | Az alagút még nem épült fel, vagy megszakadt — várj néhány percet, vagy indítsd újra |
| A felbontás nem változott automatikusan | Várj ~10 másodpercet; győződj meg róla, hogy a böngészőablak mérete tényleg változott; egyes nem szabványos felbontásokat a GPU nem támogat, ilyenkor a legközelebbit választja |

## 🛠️ Szeretnéd magad módosítani?

A munkafolyamat-fájlok a `.github/workflows/` mappában találhatók (`windows-vnc.yml` a normál kiadáshoz, `windows-vnc-rustdesk.yml` a RustDesk kiadáshoz) — közvetlenül a GitHub weboldalán szerkesztheted őket; a változások a commit után lépnek érvénybe.
