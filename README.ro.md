[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Čeština](README.cs.md) | [Dansk](README.da.md) | [Deutsch](README.de.md) | [Esperanto](README.eo.md) | [فارسی](README.fa.md) | [Suomi](README.fi.md) | [Français](README.fr.md) | [Ελληνικά](README.gr.md) | [Magyar](README.hu.md) | [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [മലയാളം](README.ml.md) | [Nederlands](README.nl.md) | [Norsk](README.no.md) | [Polski](README.pl.md) | [Português](README.ptbr.md) | [Română](README.ro.md) | [Türkçe](README.tr.md) | [Українська](README.ua.md) | [Tiếng Việt](README.vn.md)

# ☁️ Cloud-Windows — Desktop Windows gratuit în cloud

Transformă o mașină virtuală Windows gratuită din GitHub Actions într-un desktop în cloud accesibil din browser. Deschide o pagină web și ai un PC cu Windows — închide-l când ai terminat. Complet gratuit.

## ✨ Funcționalități

- 🖥️ Un desktop Windows complet, chiar în browserul tău (client web noVNC)
- 📐 **Rezoluție automată**: după ce deschizi pagina, rezoluția desktopului se potrivește automat cu dimensiunea ferestrei browserului — telefoanele și PC-urile primesc fiecare afișarea potrivită; urmărește și redimensionarea ferestrei
- 🌐 Acces prin Cloudflare Tunnel — fără IP public, fără NAT traversal
- ⌨️ IME Sogou Pinyin integrat, introducerea textului chinezesc funcționează din prima (apasă `Win + Space` pentru a comuta între chineză și engleză)
- 🖱️ Conectează-te de pe telefon, tabletă sau computer
- ⏱️ Fiecare rulare durează până la ~6 ore și o poți anula oricând
- 📦 **Ediția RustDesk**: există și un workflow RustDesk care descarcă automat cel mai recent instalator RustDesk pe Desktop (când ai nevoie de control la distanță, instalează-l singur sau folosește versiunea portabilă)

## 🚀 Utilizare (funcționează imediat după fork)

### Pasul 1: Fă fork la acest proiect

Apasă butonul **Fork** din colțul din dreapta sus al acestei pagini pentru a copia proiectul în contul tău GitHub (fă fork pe ramura `main`, nu selecta ramura `test` — este doar pentru teste). După fork, vei ajunge în depozitul `your-username/Cloud-Windows`.

> 💡 De ce fork? GitHub Actions poate rula doar în depozite din contul tău — fork-ul îți dă permisiunea să-l rulezi.

### Pasul 2: Pornește desktopul din cloud

1. Mergi la pagina depozitului tău cu fork și apasă fila **Actions** din partea de sus
2. Alege un workflow din stânga (alege unul):
   - **Windows Cloud Desktop**: desktopul standard în cloud
   - **Windows Cloud Desktop + RustDesk**: ediția standard plus descărcarea automată a celui mai recent instalator RustDesk (`rustdesk-x.x.x-x86_64.exe`) pe Desktop (versiunea nu este fixată — preia întotdeauna ultima versiune oficială); când ai nevoie de control la distanță cu RustDesk, dă dublu-clic pentru a-l instala singur sau rulează direct versiunea portabilă RustDesk
3. Apasă butonul **Run workflow** din dreapta — apare o fereastră de dialog cu trei câmpuri de intrare:

| Parametru | Descriere |
|------|------|
| VNC password | Parola pe care o vei introduce la conectarea la desktop — doar litere și cifre, maximum 8 caractere (ex. `abc12345`). **Noteaz-o** |
| Run duration | Câte minute rămâne activă această sesiune de desktop în cloud. Implicit 300 (5 ore), maximum 350 |
| Resolution | Rezoluția inițială a desktopului, implicit 1920x1080; odată ce deschizi pagina în browser, se ajustează automat la dimensiunea ferestrei |

4. Apasă butonul verde **Run workflow** pentru a confirma — desktopul din cloud începe să pornească

### Pasul 3: Obține URL-ul de acces

1. Pe pagina Actions, intră în rularea pe care tocmai ai pornit-o (cea de sus — un punct galben înseamnă că rulează)
2. Așteaptă aproximativ 3–5 minute ca mașina virtuală să instaleze software-ul și să configureze tunelul
3. Apasă pe pasul **启动服务并建立隧道**, extinde logurile și derulează în jos pentru a găsi un URL ca acesta:

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. Copiază URL-ul și deschide-l în browserul tău (browserul nativ al telefonului merge bine)

### Pasul 4: Conectează-te la desktop

1. Pe pagina noVNC care se deschide, apasă **Connect**
2. Introdu parola VNC setată la Pasul 2
3. Ești înăuntru — bucură-te de desktopul Windows 🎉
4. Rezoluția desktopului se va potrivi automat la fereastra browserului în aproximativ 10 secunde de la deschiderea paginii; redimensionarea ferestrei declanșează o reajustare automată (aleasă dintre rezoluțiile suportate de GPU-ul tău)

> ⌨️ Apasă **Win + Space** pentru a comuta metoda de introducere între Sogou Pinyin și tastatura engleză.

### Pasul 5: Închide-l când ai terminat

- Întoarce-te pe pagina Actions, deschide rularea și apasă **Cancel run** în colțul din dreapta sus — mașina virtuală este distrusă și tunelul cade
- Se încheie și automat odată ce durata setată expiră, deci nu-ți face griji că ar rula la nesfârșit

## ⚠️ Note

- **URL-ul se schimbă la fiecare rulare**: URL-ul vechi nu mai funcționează imediat ce rularea anterioară se încheie, așa că folosește întotdeauna URL-ul din logurile celei mai recente rulări
- **Nimic nu se salvează**: odată ce mașina virtuală este distrusă, fișierele, descărcările și stările de autentificare de pe desktop sunt șterse — mută fișierele importante la timp
- **Reguli de parolă**: doar litere și cifre, maximum 8 caractere — parolele mai lungi sau cu caractere speciale pot eșua la conectare (cu `Authentication failed`)
- **Nu apăsa Re-run**: pentru a porni un desktop nou, apasă **Run workflow** — Re-run redă codul vechi
- **Conexiune lentă/sacadată**: tunelul trece prin Cloudflare; vitezele din China continentală depind de rețeaua ta, dar este utilizabil
- **Pagina nu se deschide**: verifică mai întâi dacă rularea este încă în curs (punct galben) — dacă a fost anulată sau s-a terminat, URL-ul este mort

## ❓ Întrebări frecvente

| Simptom | Cauză / Remediere |
|------|-----------|
| `loopback connections are not enabled` | Bug de versiune veche — pornește o rulare nouă cu cel mai recent cod via Run workflow |
| `Server is not configured properly` | Bug de versiune veche — pornește o rulare nouă cu cel mai recent cod via Run workflow |
| `Authentication failed` | Parolă VNC greșită sau parola are peste 8 caractere / conține caractere speciale |
| 502 / 1033 în pagină | Tunelul nu e încă pornit sau a căzut — așteaptă câteva minute sau rulează din nou |
| Rezoluția nu s-a schimbat automat | Așteaptă ~10 secunde; asigură-te că fereastra browserului și-a schimbat efectiv dimensiunea; unele rezoluții nestandard nu sunt suportate de GPU și este aleasă cea mai apropiată |

## 🛠️ Vrei să-l personalizezi singur?

Fișierele de workflow se află în `.github/workflows/` (`windows-vnc.yml` pentru ediția standard, `windows-vnc-rustdesk.yml` pentru ediția RustDesk) — le poți edita chiar pe site-ul GitHub; modificările intră în vigoare după commit.
