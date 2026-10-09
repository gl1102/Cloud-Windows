[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md)

# ☁️ Cloud-Windows — Free Cloud Windows Desktop

Turn a free GitHub Actions Windows VM into a cloud desktop you can access from your browser. Open a web page and you've got a Windows PC — shut it down when you're done. Completely free.

## ✨ Features

- 🖥️ A full Windows desktop, right in your browser (noVNC web client)
- 📐 **Auto resolution**: after opening the page, the desktop resolution automatically matches your browser window size — phones and PCs each get the right fit; it follows along when you resize the window too
- 🌐 Access via Cloudflare Tunnel — no public IP, no NAT traversal needed
- ⌨️ Built-in Sogou Pinyin IME, Chinese input works out of the box (press `Win + Space` to switch between Chinese and English)
- 🖱️ Connect from your phone, tablet, or computer
- ⏱️ Each run lasts up to ~6 hours, and you can cancel anytime
- 📦 **RustDesk edition**: there's also a RustDesk workflow that automatically downloads the latest RustDesk installer to the Desktop

## 🚀 Usage (works right after forking)

### Step 1: Fork this project

Click the **Fork** button in the top-right corner of this page to copy the project to your own GitHub account. Once forked, you'll land in the `your-username/Cloud-Windows` repository.

> 💡 Why fork? GitHub Actions can only run in repositories under your own account — forking gives you permission to run it.

### Step 2: Launch the cloud desktop

1. Go to your forked repo's page and click the **Actions** tab at the top
2. Choose a workflow on the left (pick one):
   - **Windows Cloud Desktop**: the standard cloud desktop
   - **Windows Cloud Desktop + RustDesk**: standard edition plus automatic download of the latest RustDesk installer to the Desktop (version not hardcoded — always fetches the latest official release)
3. Click the **Run workflow** button on the right — a dialog with three inputs pops up:

| Parameter | Description |
|------|------|
| VNC password | The password you'll enter when connecting to the desktop — letters and numbers only, up to 8 characters (e.g. `abc12345`). **Write it down** |
| Run duration | How many minutes this cloud desktop session stays alive. Default 300 (5 hours), max 350 |
| Resolution | The initial desktop resolution, default 1920x1080; once you open the page in your browser it auto-adjusts to your window size |

4. Click the green **Run workflow** to confirm — the cloud desktop starts booting

### Step 3: Get the access URL

1. On the Actions page, click into the run you just started (the topmost one — a yellow dot means it's running)
2. Wait about 3–5 minutes for the VM to install software and set up the tunnel
3. Click the **启动服务并建立隧道** step, expand the logs, and scroll down to find a URL like this:

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. Copy the URL and open it in your browser (your phone's built-in browser works fine)

### Step 4: Connect to the desktop

1. On the noVNC page that opens, click **Connect**
2. Enter the VNC password you set in Step 2
3. You're in — enjoy your Windows desktop 🎉
4. The desktop resolution will auto-fit your browser window within about 10 seconds of opening the page; resizing the window triggers an automatic re-fit (chosen from the resolutions your GPU supports)

> ⌨️ Press **Win + Space** to switch the input method between Sogou Pinyin and the English keyboard.

### Step 5: Shut it down when you're done

- Go back to the Actions page, open the run, and click **Cancel run** in the top-right — the VM is destroyed and the tunnel goes dead
- It also ends automatically once the set duration elapses, so no worries about it running forever

## ⚠️ Notes

- **The URL changes every run**: the old URL stops working as soon as the previous run ends, so always use the URL from the latest run's logs
- **Nothing is saved**: once the VM is destroyed, files, downloads, and login states on the desktop are all wiped — move important files out in time
- **Password rules**: letters and numbers only, up to 8 characters — longer passwords or ones with special characters may fail to connect (with `Authentication failed`)
- **Don't click Re-run**: to start a new desktop, click **Run workflow** — Re-run replays old code
- **Slow/laggy connection**: the tunnel goes through Cloudflare; speeds from mainland China depend on your network, but it's usable
- **Page won't open**: first check the run is still in progress (yellow dot) — if it's been canceled or finished, the URL is dead

## ❓ FAQ

| Symptom | Cause / Fix |
|------|-----------|
| `loopback connections are not enabled` | Old-version bug — start a fresh run with the latest code via Run workflow |
| `Server is not configured properly` | Old-version bug — start a fresh run with the latest code via Run workflow |
| `Authentication failed` | Wrong VNC password, or the password is over 8 characters / contains special characters |
| 502 / 1033 in the page | Tunnel isn't up yet or has dropped — wait a few minutes or run again |
| Resolution didn't auto-change | Wait ~10 seconds; make sure the browser window actually changed size; some non-standard resolutions aren't supported by the GPU and the closest one is picked instead |

## 🛠️ Want to tweak it yourself?

The workflow files live under `.github/workflows/` (`windows-vnc.yml` for the standard edition, `windows-vnc-rustdesk.yml` for the RustDesk edition) — you can edit them right on the GitHub website; changes take effect after you commit.
