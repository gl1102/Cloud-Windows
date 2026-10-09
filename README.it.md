[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Čeština](README.cs.md) | [Dansk](README.da.md) | [Deutsch](README.de.md) | [Esperanto](README.eo.md) | [فارسی](README.fa.md) | [Suomi](README.fi.md) | [Français](README.fr.md) | [Ελληνικά](README.gr.md) | [Magyar](README.hu.md) | [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [മലയാളം](README.ml.md) | [Nederlands](README.nl.md) | [Norsk](README.no.md) | [Polski](README.pl.md) | [Português](README.ptbr.md) | [Română](README.ro.md) | [Türkçe](README.tr.md) | [Українська](README.ua.md) | [Tiếng Việt](README.vn.md)

# ☁️ Cloud-Windows — Desktop Windows cloud gratuito

Trasforma una VM Windows gratuita di GitHub Actions in un desktop cloud accessibile dal browser. Apri una pagina web e avrai un PC Windows — spegnilo quando hai finito. Completamente gratuito.

## ✨ Funzionalità

- 🖥️ Un desktop Windows completo, direttamente nel browser (client web noVNC)
- 📐 **Risoluzione automatica**: dopo aver aperto la pagina, la risoluzione del desktop si adatta automaticamente alle dimensioni della finestra del browser — telefoni e PC ottengono ciascuno la dimensione giusta; segue anche quando ridimensioni la finestra
- 🌐 Accesso tramite Cloudflare Tunnel — niente IP pubblico, niente NAT traversal
- ⌨️ Metodo di input Sogou Pinyin integrato, l'input cinese funziona subito (premi `Win + Space` per passare tra cinese e inglese)
- 🖱️ Connettiti da telefono, tablet o computer
- ⏱️ Ogni sessione dura fino a ~6 ore, e puoi annullarla in qualsiasi momento
- 📦 **Edizione RustDesk**: esiste anche un workflow RustDesk che scarica automaticamente il programma di installazione dell'ultima versione di RustDesk sul Desktop (per il controllo remoto, installalo tu stesso oppure usa la versione portable)

## 🚀 Uso (funziona subito dopo il fork)

### Passo 1: Fai il fork di questo progetto

Clicca sul pulsante **Fork** in alto a destra di questa pagina per copiare il progetto nel tuo account GitHub (il fork copia il branch `main` — non selezionare il branch `test`, che serve solo per i test). Dopo il fork, arriverai nel repository `your-username/Cloud-Windows`.

> 💡 Perché il fork? GitHub Actions può essere eseguito solo nei repository del tuo account — il fork ti dà il permesso di eseguirlo.

### Passo 2: Avvia il desktop cloud

1. Vai alla pagina del tuo repository forkato e clicca sulla scheda **Actions** in alto
2. Scegli un workflow a sinistra (scegline uno):
   - **Windows Cloud Desktop**: il desktop cloud standard
   - **Windows Cloud Desktop + RustDesk**: edizione standard più download automatico del programma di installazione dell'ultima versione di RustDesk (`rustdesk-x.x.x-x86_64.exe`) sul Desktop (versione non hardcoded — scarica sempre l'ultima release ufficiale); per il controllo remoto con RustDesk, fai doppio clic per installarlo, oppure esegui direttamente la versione portable di RustDesk senza installazione
3. Clicca sul pulsante **Run workflow** a destra — si apre una finestra di dialogo con tre campi di input:

| Parametro | Descrizione |
|------|------|
| Password VNC | La password che inserirai per connetterti al desktop — solo lettere e numeri, massimo 8 caratteri (es. `abc12345`). **Segnala** |
| Durata sessione | Quanti minuti questa sessione di desktop cloud rimane attiva. Predefinito 300 (5 ore), massimo 350 |
| Risoluzione | La risoluzione iniziale del desktop, predefinita 1920x1080; una volta aperta la pagina nel browser si adatta automaticamente alle dimensioni della finestra |

4. Clicca sul pulsante verde **Run workflow** per confermare — il desktop cloud inizia l'avvio

### Passo 3: Ottieni l'URL di accesso

1. Nella pagina Actions, clicca sulla sessione appena avviata (quella in alto — il pallino giallo significa che è in esecuzione)
2. Attendi circa 3–5 minuti affinché la VM installi il software e configuri il tunnel
3. Clicca sullo step **启动服务并建立隧道**, espandi i log e scorri verso il basso per trovare un URL come questo:

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. Copia l'URL e aprilo nel browser (va bene anche il browser integrato del telefono)

### Passo 4: Connettiti al desktop

1. Nella pagina noVNC che si apre, clicca su **Connect**
2. Inserisci la password VNC impostata al Passo 2
3. Ci sei — buon divertimento con il tuo desktop Windows 🎉
4. La risoluzione del desktop si adatterà automaticamente alla finestra del browser entro circa 10 secondi dall'apertura della pagina; ridimensionare la finestra attiva un nuovo adattamento automatico (scelto tra le risoluzioni supportate dalla tua GPU)

> ⌨️ Premi **Win + Space** per passare il metodo di input tra Sogou Pinyin e la tastiera inglese.

### Passo 5: Spegnilo quando hai finito

- Torna alla pagina Actions, apri la sessione e clicca su **Cancel run** in alto a destra — la VM viene distrutta e il tunnel si interrompe
- Termina anche automaticamente una volta trascorsa la durata impostata, quindi nessun problema

## ⚠️ Note

- **L'URL cambia a ogni sessione**: il vecchio URL smette di funzionare non appena la sessione precedente termina, quindi usa sempre l'URL dai log dell'ultima sessione
- **Non viene salvato nulla**: una volta distrutta la VM, file, download e stati di accesso sul desktop vengono tutti cancellati — sposta in tempo i file importanti
- **Regole password**: solo lettere e numeri, massimo 8 caratteri — password più lunghe o con caratteri speciali potrebbero fallire la connessione (con `Authentication failed`)
- **Non cliccare Re-run**: per avviare un nuovo desktop, clicca su **Run workflow** — Re-run riesegue il vecchio codice
- **Connessione lenta/lag**: il tunnel passa attraverso Cloudflare; le velocità dalla Cina continentale dipendono dalla tua rete, ma è utilizzabile
- **La pagina non si apre**: prima controlla che la sessione sia ancora in esecuzione (pallino giallo) — se è stata annullata o è terminata, l'URL è morto

## ❓ FAQ

| Sintomo | Causa / Soluzione |
|------|-----------|
| `loopback connections are not enabled` | Bug di una vecchia versione — avvia una nuova sessione con il codice più recente tramite Run workflow |
| `Server is not configured properly` | Bug di una vecchia versione — avvia una nuova sessione con il codice più recente tramite Run workflow |
| `Authentication failed` | Password VNC errata, oppure password oltre 8 caratteri / con caratteri speciali |
| 502 / 1033 nella pagina | Il tunnel non è ancora attivo o è caduto — attendi qualche minuto o riavvia |
| La risoluzione non è cambiata automaticamente | Attendi ~10 secondi; assicurati che le dimensioni della finestra del browser siano cambiate davvero; alcune risoluzioni non standard non sono supportate dalla GPU e viene scelta la più vicina |

## 🛠️ Vuoi modificarlo da solo?

I file di workflow si trovano in `.github/workflows/` (`windows-vnc.yml` per l'edizione standard, `windows-vnc-rustdesk.yml` per l'edizione RustDesk) — puoi modificarli direttamente sul sito GitHub; le modifiche hanno effetto dopo il commit.
