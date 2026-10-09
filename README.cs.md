[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Čeština](README.cs.md) | [Dansk](README.da.md) | [Deutsch](README.de.md) | [Esperanto](README.eo.md) | [فارسی](README.fa.md) | [Suomi](README.fi.md) | [Français](README.fr.md) | [Ελληνικά](README.gr.md) | [Magyar](README.hu.md) | [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [മലയാളം](README.ml.md) | [Nederlands](README.nl.md) | [Norsk](README.no.md) | [Polski](README.pl.md) | [Português](README.ptbr.md) | [Română](README.ro.md) | [Türkçe](README.tr.md) | [Українська](README.ua.md) | [Tiếng Việt](README.vn.md)

# ☁️ Cloud-Windows — Bezplatná cloudová plocha Windows

Proměňte bezplatný virtuální stroj Windows v GitHub Actions v cloudovou plochu přístupnou z prohlížeče. Otevřete webovou stránku a máte počítač s Windows — až skončíte, vypněte ho. Zcela zdarma.

## ✨ Funkce

- 🖥️ Plná plocha Windows přímo ve vašem prohlížeči (webový klient noVNC)
- 📐 **Automatické rozlišení**: po otevření stránky se rozlišení plochy automaticky přizpůsobí velikosti okna prohlížeče — telefony i počítače dostanou správnou velikost; přizpůsobí se i při změně velikosti okna
- 🌐 Přístup přes Cloudflare Tunnel — není potřeba veřejná IP adresa ani procházení NAT
- ⌨️ Vestavěná čínská metoda zadávání Sogou Pinyin, čínský vstup funguje okamžitě (stisknutím `Win + Space` přepínáte mezi čínštinou a angličtinou)
- 🖱️ Připojte se z telefonu, tabletu nebo počítače
- ⏱️ Každé spuštění vydrží až ~6 hodin a můžete ho kdykoli zrušit
- 📦 **Edice RustDesk**: je k dispozici i workflow RustDesk, který automaticky stáhne nejnovější RustDesk na disk D a tiše ho nainstaluje do `D:\RustDesk`

## 🚀 Použití (funguje hned po forknutí)

### Krok 1: Forkněte tento projekt

Klikněte na tlačítko **Fork** v pravém horním rohu této stránky a zkopírujte projekt do svého účtu GitHub. Po forku se ocitnete v repozitáři `your-username/Cloud-Windows`.

> 💡 Proč fork? GitHub Actions mohou běžet jen v repozitářích pod vaším účtem — forknutím získáte oprávnění je spouštět.

### Krok 2: Spusťte cloudovou plochu

1. Přejděte na stránku svého forknutého repozitáře a klikněte nahoře na kartu **Actions**
2. Vlevo vyberte workflow (vyberte jeden):
   - **Windows Cloud Desktop**: standardní cloudová plocha
   - **Windows Cloud Desktop + RustDesk**: standardní edice plus automatické stažení nejnovějšího RustDesku na disk D s tichou instalací do `D:\RustDesk` (verze není napevno zadaná — vždy stahuje nejnovější oficiální vydání)
3. Klikněte vpravo na tlačítko **Run workflow** — objeví se dialog se třemi vstupy:

| Parametr | Popis |
|------|------|
| Heslo VNC | Heslo, které zadáte při připojování k ploše — pouze písmena a čísla, maximálně 8 znaků (např. `abc12345`). **Poznamenejte si ho** |
| Doba běhu | Kolik minut zůstane cloudová plocha aktivní. Výchozí 300 (5 hodin), maximum 350 |
| Rozlišení | Počáteční rozlišení plochy, výchozí 1920x1080; jakmile otevřete stránku v prohlížeči, automaticky se přizpůsobí velikosti vašeho okna |

4. Klikněte na zelené tlačítko **Run workflow** pro potvrzení — cloudová plocha se začne spouštět

### Krok 3: Získejte přístupovou URL

1. Na stránce Actions klikněte na spuštění, které jste právě spustili (nejhornější — žlutá tečka znamená, že běží)
2. Počkejte asi 3–5 minut, než virtuální stroj nainstaluje software a nastaví tunel
3. Klikněte na krok **启动服务并建立隧道**, rozbalte logy a sjeďte dolů, abyste našli URL podobnou této:

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. URL zkopírujte a otevřete v prohlížeči (vestavěný prohlížeč v telefonu funguje dobře)

### Krok 4: Připojte se k ploše

1. Na otevřené stránce noVNC klikněte na **Connect**
2. Zadejte heslo VNC, které jste nastavili v kroku 2
3. Jste uvnitř — užijte si plochu Windows 🎉
4. Rozlišení plochy se automaticky přizpůsobí oknu prohlížeče přibližně do 10 sekund po otevření stránky; změna velikosti okna spustí automatické přizpůsobení (vybírá se z rozlišení, která podporuje vaše GPU)

> ⌨️ Stisknutím **Win + Space** přepínáte metodu zadávání mezi Sogou Pinyin a anglickou klávesnicí.

### Krok 5: Až skončíte, vypněte ji

- Vraťte se na stránku Actions, otevřete spuštění a klikněte vpravo nahoře na **Cancel run** — virtuální stroj se zničí a tunel přestane fungovat
- Skončí také automaticky po uplynutí nastavené doby, takže se nemusíte bát, že poběží věčně

## ⚠️ Poznámky

- **URL se mění při každém spuštění**: stará URL přestane fungovat, jakmile skončí předchozí spuštění, takže vždy používejte URL z logů nejnovějšího spuštění
- **Nic se neukládá**: jakmile je virtuální stroj zničen, soubory, stažené soubory a přihlášené relace na ploše jsou všechny smazány — důležité soubory si včas přeneste ven
- **Pravidla pro heslo**: pouze písmena a čísla, maximálně 8 znaků — delší hesla nebo hesla se speciálními znaky se nemusí připojit (s chybou `Authentication failed`)
- **Neklikejte na Re-run**: pro spuštění nové plochy klikněte na **Run workflow** — Re-run přehrává starý kód
- **Pomalé/zasekávající se připojení**: tunel prochází přes Cloudflare; rychlosti z pevninské Číny závisí na vaší síti, ale je použitelný
- **Stránka se neotevře**: nejprve zkontrolujte, zda spuštění stále běží (žlutá tečka) — pokud bylo zrušeno nebo skončilo, je URL mrtvá

## ❓ Časté dotazy

| Příznak | Příčina / řešení |
|------|-----------|
| `loopback connections are not enabled` | Chyba staré verze — spusťte nové spuštění s nejnovějším kódem přes Run workflow |
| `Server is not configured properly` | Chyba staré verze — spusťte nové spuštění s nejnovějším kódem přes Run workflow |
| `Authentication failed` | Špatné heslo VNC, nebo je delší než 8 znaků / obsahuje speciální znaky |
| 502 / 1033 na stránce | Tunel ještě není nahoře nebo vypadl — počkejte pár minut nebo spusťte znovu |
| Rozlišení se automaticky nezměnilo | Počkejte ~10 sekund; ujistěte se, že se velikost okna prohlížeče skutečně změnila; některá nestandardní rozlišení GPU nepodporuje a vybere se nejbližší možné |

## 🛠️ Chcete si to upravit sami?

Soubory workflow jsou v `.github/workflows/` (`windows-vnc.yml` pro standardní edici, `windows-vnc-rustdesk.yml` pro edici RustDesk) — můžete je upravit přímo na webu GitHub; změny se projeví po commitu.
