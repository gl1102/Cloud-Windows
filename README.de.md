[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Čeština](README.cs.md) | [Dansk](README.da.md) | [Deutsch](README.de.md) | [Esperanto](README.eo.md) | [فارسی](README.fa.md) | [Suomi](README.fi.md) | [Français](README.fr.md) | [Ελληνικά](README.gr.md) | [Magyar](README.hu.md) | [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [മലയാളം](README.ml.md) | [Nederlands](README.nl.md) | [Norsk](README.no.md) | [Polski](README.pl.md) | [Português](README.ptbr.md) | [Română](README.ro.md) | [Türkçe](README.tr.md) | [Українська](README.ua.md) | [Tiếng Việt](README.vn.md)

# ☁️ Cloud-Windows — Kostenloser Cloud-Windows-Desktop

Verwandle eine kostenlose GitHub-Actions-Windows-VM in einen Cloud-Desktop, auf den du vom Browser aus zugreifen kannst. Öffne eine Webseite und du hast einen Windows-PC — fahr ihn herunter, wenn du fertig bist. Komplett kostenlos.

## ✨ Funktionen

- 🖥️ Ein vollständiger Windows-Desktop, direkt in deinem Browser (noVNC-Webclient)
- 📐 **Automatische Auflösung**: Nach dem Öffnen der Seite passt sich die Desktop-Auflösung automatisch an die Größe deines Browserfensters an — Handys und PCs bekommen jeweils die richtige Anpassung; sie folgt auch mit, wenn du die Fenstergröße änderst
- 🌐 Zugriff über Cloudflare Tunnel — keine öffentliche IP, kein NAT-Traversal nötig
- ⌨️ Eingebaute Sogou-Pinyin-Eingabemethode, chinesische Eingabe funktioniert sofort (`Win + Space` drücken, um zwischen Chinesisch und Englisch zu wechseln)
- 🖱️ Von Handy, Tablet oder Computer verbinden
- ⏱️ Jeder Durchlauf dauert bis zu ~6 Stunden, und du kannst jederzeit abbrechen
- 📦 **RustDesk-Edition**: Es gibt auch einen RustDesk-Workflow, der automatisch das neueste RustDesk-Installationsprogramm auf den Desktop herunterlädt (bei Bedarf an Fernsteuerung selbst installieren oder die portable Version verwenden)

## 🚀 Verwendung (funktioniert direkt nach dem Forken)

### Schritt 1: Forke dieses Projekt

Klicke oben rechts auf dieser Seite auf den **Fork**-Button, um das Projekt in dein eigenes GitHub-Konto zu kopieren (geforkt wird der `main`-Branch — wähle nicht den `test`-Branch, der ist nur zum Testen). Nach dem Forken landest du im Repository `your-username/Cloud-Windows`.

> 💡 Warum forken? GitHub Actions kann nur in Repositories unter deinem eigenen Konto laufen — durch das Forken erhältst du die Berechtigung, es auszuführen.

### Schritt 2: Starte den Cloud-Desktop

1. Gehe auf die Seite deines geforkten Repos und klicke oben auf den **Actions**-Tab
2. Wähle links einen Workflow aus (einen auswählen):
   - **Windows Cloud Desktop**: der Standard-Cloud-Desktop
   - **Windows Cloud Desktop + RustDesk**: Standard-Edition plus automatischer Download des neuesten RustDesk-Installationsprogramms (`rustdesk-x.x.x-x86_64.exe`) auf den Desktop (Version nicht fest kodiert — lädt immer das neueste offizielle Release); für die Fernsteuerung mit RustDesk einfach selbst doppelklicken, um zu installieren, oder die portable RustDesk-Version ohne Installation direkt ausführen
3. Klicke rechts auf den **Run workflow**-Button — ein Dialog mit drei Eingabefeldern öffnet sich:

| Parameter | Beschreibung |
|------|------|
| VNC-Passwort | Das Passwort, das du bei der Verbindung zum Desktop eingibst — nur Buchstaben und Zahlen, bis zu 8 Zeichen (z. B. `abc12345`). **Notiere es dir** |
| Laufzeit | Wie viele Minuten diese Cloud-Desktop-Sitzung aktiv bleibt. Standard 300 (5 Stunden), max. 350 |
| Auflösung | Die anfängliche Desktop-Auflösung, Standard 1920x1080; sobald du die Seite in deinem Browser öffnest, passt sie sich automatisch an deine Fenstergröße an |

4. Klicke zur Bestätigung auf den grünen **Run workflow**-Button — der Cloud-Desktop beginnt zu booten

### Schritt 3: Hol dir die Zugriffs-URL

1. Klicke auf der Actions-Seite in den Lauf, den du gerade gestartet hast (der oberste — ein gelber Punkt bedeutet, dass er läuft)
2. Warte etwa 3–5 Minuten, bis die VM Software installiert und den Tunnel eingerichtet hat
3. Klicke auf den Schritt **启动服务并建立隧道**, klappe die Logs auf und scrolle nach unten, um eine URL wie diese zu finden:

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. Kopiere die URL und öffne sie in deinem Browser (der eingebaute Browser deines Handys funktioniert einwandfrei)

### Schritt 4: Verbinde dich mit dem Desktop

1. Klicke auf der geöffneten noVNC-Seite auf **Connect**
2. Gib das VNC-Passwort ein, das du in Schritt 2 festgelegt hast
3. Du bist drin — viel Spaß mit deinem Windows-Desktop 🎉
4. Die Desktop-Auflösung passt sich innerhalb von etwa 10 Sekunden nach dem Öffnen der Seite automatisch an dein Browserfenster an; eine Größenänderung des Fensters löst eine automatische Neuanpassung aus (ausgewählt aus den Auflösungen, die deine GPU unterstützt)

> ⌨️ Drücke **Win + Space**, um die Eingabemethode zwischen Sogou Pinyin und der englischen Tastatur zu wechseln.

### Schritt 5: Fahr ihn herunter, wenn du fertig bist

- Gehe zurück auf die Actions-Seite, öffne den Lauf und klicke oben rechts auf **Cancel run** — die VM wird zerstört und der Tunnel ist tot
- Er endet auch automatisch, sobald die eingestellte Dauer abgelaufen ist, also keine Sorge, dass er ewig läuft

## ⚠️ Hinweise

- **Die URL ändert sich bei jedem Lauf**: Die alte URL funktioniert nicht mehr, sobald der vorherige Lauf endet, also verwende immer die URL aus den Logs des neuesten Laufs
- **Nichts wird gespeichert**: Sobald die VM zerstört ist, werden Dateien, Downloads und Anmeldezustände auf dem Desktop alle gelöscht — bringe wichtige Dateien rechtzeitig in Sicherheit
- **Passwortregeln**: Nur Buchstaben und Zahlen, bis zu 8 Zeichen — längere Passwörter oder solche mit Sonderzeichen können die Verbindung fehlschlagen lassen (mit `Authentication failed`)
- **Klicke nicht auf Re-run**: Um einen neuen Desktop zu starten, klicke auf **Run workflow** — Re-run spielt alten Code ab
- **Langsame/ruckelnde Verbindung**: Der Tunnel läuft über Cloudflare; die Geschwindigkeiten vom chinesischen Festland hängen von deinem Netzwerk ab, aber er ist nutzbar
- **Seite öffnet sich nicht**: Prüfe zuerst, ob der Lauf noch läuft (gelber Punkt) — wenn er abgebrochen oder beendet ist, ist die URL tot

## ❓ FAQ

| Symptom | Ursache / Lösung |
|------|-----------|
| `loopback connections are not enabled` | Fehler in alter Version — starte einen neuen Lauf mit dem neuesten Code über Run workflow |
| `Server is not configured properly` | Fehler in alter Version — starte einen neuen Lauf mit dem neuesten Code über Run workflow |
| `Authentication failed` | Falsches VNC-Passwort, oder das Passwort ist länger als 8 Zeichen / enthält Sonderzeichen |
| 502 / 1033 auf der Seite | Tunnel ist noch nicht oben oder abgebrochen — warte ein paar Minuten oder starte erneut |
| Auflösung hat sich nicht automatisch geändert | Warte ~10 Sekunden; stelle sicher, dass sich die Browserfenstergröße tatsächlich geändert hat; manche Nicht-Standard-Auflösungen werden von der GPU nicht unterstützt und die nächstliegende wird stattdessen gewählt |

## 🛠️ Willst du es selbst anpassen?

Die Workflow-Dateien liegen unter `.github/workflows/` (`windows-vnc.yml` für die Standard-Edition, `windows-vnc-rustdesk.yml` für die RustDesk-Edition) — du kannst sie direkt auf der GitHub-Website bearbeiten; Änderungen werden nach dem Commit wirksam.
