[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Čeština](README.cs.md) | [Dansk](README.da.md) | [Deutsch](README.de.md) | [Esperanto](README.eo.md) | [فارسی](README.fa.md) | [Suomi](README.fi.md) | [Français](README.fr.md) | [Ελληνικά](README.gr.md) | [Magyar](README.hu.md) | [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [മലയാളം](README.ml.md) | [Nederlands](README.nl.md) | [Norsk](README.no.md) | [Polski](README.pl.md) | [Português](README.ptbr.md) | [Română](README.ro.md) | [Türkçe](README.tr.md) | [Українська](README.ua.md) | [Tiếng Việt](README.vn.md)

# ☁️ Cloud-Windows — Senpaga Nuba Vindoza Labortablo

Transformu senpagan GitHub Actions Vindozan VM-on en nubolan labortablon, alireblan el via retumilo. Malfermu retpaĝon kaj vi havas Vindozan komputilon — malŝaltu ĝin kiam vi finos. Tute senpage.

## ✨ Ecoj

- 🖥️ Plena Vindoza labortablo, rekte en via retumilo (noVNC retkliento)
- 📐 **Aŭtomata rezolucio**: post malfermo de la paĝo, la labortabla rezolucio aŭtomate kongruas kun la grandeco de via retumila fenestro — telefonoj kaj komputiloj ĉiu ricevas taŭgan adapton; ĝi sekvas ankaŭ kiam vi ŝanĝas la fenestrograndon
- 🌐 Aliro per Cloudflare Tunnel — neniu publika IP bezonata, neniu NAT-trairo bezonata
- ⌨️ Enkonstruita ĉina eniga metodo Sogou Pinyin, ĉina enigo funkcias tuj (premu `Win + Space` por ŝanĝi inter la ĉina kaj la angla)
- 🖱️ Konektiĝu de via telefono, tablojdo aŭ komputilo
- ⏱️ Ĉiu rulo daŭras ĝis ~6 horoj, kaj vi povas nuligi iam ajn
- 📦 **RustDesk-eldono**: ekzistas ankaŭ RustDesk-laborfluo kiu aŭtomate elŝutas la plej novan RustDesk al la D-disko kaj silente instalas ĝin al `D:\RustDesk`

## 🚀 Uzo (funkcias tuj post forko)

### Paŝo 1: Forku ĉi tiun projekton

Alklaku la butonon **Fork** en la supradekstra angulo de ĉi tiu paĝo por kopii la projekton al via propra GitHub-konto. Post forko vi alvenos en la deponejon `your-username/Cloud-Windows`.

> 💡 Kial forki? GitHub Actions povas funkcii nur en deponejoj sub via propra konto — forko donas al vi permeson funkciigi ĝin.

### Paŝo 2: Lanĉu la nubolan labortablon

1. Iru al la paĝo de via forkita deponejo kaj alklaku la langeton **Actions** supre
2. Elektu laborfluon maldekstre (elektu unu):
   - **Windows Cloud Desktop**: la norma nuba labortablo
   - **Windows Cloud Desktop + RustDesk**: norma eldono plus aŭtomata elŝuto de la plej nova RustDesk al la D-disko kun silenta instalado al `D:\RustDesk` (versio ne estas fiksa — ĉiam prenas la plej novan oficialan eldonon)
3. Alklaku la butonon **Run workflow** dekstre — aperas dialogo kun tri enigaĵoj:

| Parametro | Priskribo |
|------|------|
| VNC-pasvorto | La pasvorto, kiun vi enigos dum konektiĝo al la labortablo — nur literoj kaj ciferoj, ĝis 8 signoj (ekz. `abc12345`). **Skribu ĝin** |
| Daŭro | Kiom da minutoj tiu nuba labortabla sesio restas aktiva. Defaŭlte 300 (5 horoj), maksimume 350 |
| Rezolucio | La komenca labortabla rezolucio, defaŭlte 1920x1080; post kiam vi malfermas la paĝon en via retumilo ĝi aŭtomate adaptiĝas al via fenestrograndeco |

4. Alklaku la verdan **Run workflow** por konfirmi — la nuba labortablo komencas ekfunkcii

### Paŝo 3: Akiru la alir-adreson

1. En la Actions-paĝo, alklaku en la rulon, kiun vi ĵus startigis (la plej supra — flava punkto signifas, ke ĝi funkcias)
2. Atendu ĉirkaŭ 3–5 minutojn dum la VM instalas programaron kaj agordas la tunelon
3. Alklaku la paŝon **启动服务并建立隧道**, malfaldu la protokolojn, kaj rulumu malsupren por trovi adreson kiel ĉi tiu:

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. Kopiu la adreson kaj malfermu ĝin en via retumilo (la enkonstruita retumilo de via telefono funkcias bone)

### Paŝo 4: Konektiĝu al la labortablo

1. En la malfermita noVNC-paĝo, alklaku **Connect**
2. Enigu la VNC-pasvorton, kiun vi agordis en Paŝo 2
3. Vi eniris — ĝuu vian Vindozan labortablon 🎉
4. La labortabla rezolucio aŭtomate adaptiĝos al via retumila fenestro ene de ĉirkaŭ 10 sekundoj post malfermo de la paĝo; ŝanĝo de la fenestrograndeco ekigas aŭtomatan re-adapton (elektata el la rezolucioj, kiujn via GPU subtenas)

> ⌨️ Premu **Win + Space** por ŝanĝi la enigan metodon inter Sogou Pinyin kaj la angla klavaro.

### Paŝo 5: Malŝaltu ĝin kiam vi finos

- Reiru al la Actions-paĝo, malfermu la rulon, kaj alklaku **Cancel run** supradekstre — la VM estas detruita kaj la tunelo mortas
- Ĝi ankaŭ finiĝas aŭtomate post kiam la agordita daŭro pasas, do ne zorgu pri senfina funkciado

## ⚠️ Notoj

- **La adreso ŝanĝiĝas ĉiufoje**: la malnova adreso ĉesas funkcii tuj kiam la antaŭa rulo finiĝas, do ĉiam uzu la adreson el la protokoloj de la plej nova rulo
- **Nenio estas konservita**: post detruo de la VM, dosieroj, elŝutoj, kaj ensalutaj statoj sur la labortablo estas ĉiuj forviŝitaj — movu gravajn dosierojn eksteren ĝustatempe
- **Pasvortaj reguloj**: nur literoj kaj ciferoj, ĝis 8 signoj — pli longaj pasvortoj aŭ tiuj kun specialaj signoj eble malsukcesos konektiĝi (kun `Authentication failed`)
- **Ne alklaku Re-run**: por startigi novan labortablon, alklaku **Run workflow** — Re-run reludas malnovan kodon
- **Malrapida/tremetanta konekto**: la tunelo iras tra Cloudflare; rapidecoj el kontinenta Ĉinio dependas de via reto, sed ĝi estas uzebla
- **Paĝo ne malfermiĝas**: unue kontrolu, ke la rulo ankoraŭ funkcias (flava punkto) — se ĝi estis nuligita aŭ finita, la adreso estas morta

## ❓ Oftaj demandoj

| Simptomo | Kaŭzo / Solvo |
|------|-----------|
| `loopback connections are not enabled` | Malnova-versia cimo — startigu freŝan rulon kun la plej nova kodo per Run workflow |
| `Server is not configured properly` | Malnova-versia cimo — startigu freŝan rulon kun la plej nova kodo per Run workflow |
| `Authentication failed` | Malĝusta VNC-pasvorto, aŭ la pasvorto estas pli ol 8 signoj / enhavas specialajn signojn |
| 502 / 1033 en la paĝo | Tunelo ankoraŭ ne suprenis aŭ falis — atendu kelkajn minutojn aŭ rulu denove |
| Rezolucio ne ŝanĝiĝis aŭtomate | Atendu ~10 sekundojn; certigu, ke la retumila fenestrograndeco vere ŝanĝiĝis; iuj ne-normaj rezolucioj ne estas subtenataj de la GPU kaj la plej proksima estas elektita anstataŭe |

## 🛠️ Ĉu vi volas ĝustigi ĝin mem?

La laborfluaj dosieroj troviĝas sub `.github/workflows/` (`windows-vnc.yml` por la norma eldono, `windows-vnc-rustdesk.yml` por la RustDesk-eldono) — vi povas redakti ilin rekte en la GitHub-retejo; ŝanĝoj efektiviĝas post commit.
