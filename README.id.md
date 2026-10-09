[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Čeština](README.cs.md) | [Dansk](README.da.md) | [Deutsch](README.de.md) | [Esperanto](README.eo.md) | [فارسی](README.fa.md) | [Suomi](README.fi.md) | [Français](README.fr.md) | [Ελληνικά](README.gr.md) | [Magyar](README.hu.md) | [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [മലയാളം](README.ml.md) | [Nederlands](README.nl.md) | [Norsk](README.no.md) | [Polski](README.pl.md) | [Português](README.ptbr.md) | [Română](README.ro.md) | [Türkçe](README.tr.md) | [Українська](README.ua.md) | [Tiếng Việt](README.vn.md)

# ☁️ Cloud-Windows — Desktop Windows Cloud Gratis

Ubah VM Windows gratis dari GitHub Actions menjadi desktop cloud yang bisa diakses dari browser. Buka halaman web dan Anda punya PC Windows — matikan setelah selesai. Sepenuhnya gratis.

## ✨ Fitur

- 🖥️ Desktop Windows lengkap, langsung di browser Anda (klien web noVNC)
- 📐 **Resolusi otomatis**: setelah membuka halaman, resolusi desktop otomatis menyesuaikan ukuran jendela browser Anda — ponsel dan PC masing-masing mendapatkan tampilan yang pas; mengikuti juga saat jendela diubah ukurannya
- 🌐 Akses via Cloudflare Tunnel — tanpa IP publik, tanpa perlu NAT traversal
- ⌨️ IME Sogou Pinyin bawaan, input bahasa Mandarin langsung bisa dipakai (tekan `Win + Space` untuk beralih antara Mandarin dan Inggris)
- 🖱️ Terhubung dari ponsel, tablet, atau komputer
- ⏱️ Setiap sesi berjalan hingga ~6 jam, dan bisa dibatalkan kapan saja
- 📦 **Edisi RustDesk**: ada juga workflow RustDesk yang otomatis mengunduh RustDesk terbaru ke drive D dan menginstalnya secara diam-diam ke `D:\RustDesk`

## 🚀 Penggunaan (langsung jalan setelah fork)

### Langkah 1: Fork proyek ini

Klik tombol **Fork** di kanan atas halaman ini untuk menyalin proyek ke akun GitHub Anda sendiri. Setelah di-fork, Anda akan masuk ke repositori `your-username/Cloud-Windows`.

> 💡 Kenapa fork? GitHub Actions hanya bisa berjalan di repositori di bawah akun Anda sendiri — fork memberi Anda izin untuk menjalankannya.

### Langkah 2: Luncurkan desktop cloud

1. Buka halaman repo hasil fork Anda dan klik tab **Actions** di atas
2. Pilih workflow di sebelah kiri (pilih satu):
   - **Windows Cloud Desktop**: desktop cloud standar
   - **Windows Cloud Desktop + RustDesk**: edisi standar plus unduhan otomatis RustDesk terbaru ke drive D dengan instalasi diam-diam ke `D:\RustDesk` (versi tidak di-hardcode — selalu mengambil rilis resmi terbaru)
3. Klik tombol **Run workflow** di kanan — dialog dengan tiga kolom input akan muncul:

| Parameter | Deskripsi |
|------|------|
| Kata sandi VNC | Kata sandi yang akan Anda masukkan saat menghubungkan ke desktop — huruf dan angka saja, maksimal 8 karakter (mis. `abc12345`). **Catat** |
| Durasi sesi | Berapa menit sesi desktop cloud ini tetap hidup. Default 300 (5 jam), maks 350 |
| Resolusi | Resolusi awal desktop, default 1920x1080; setelah halaman dibuka di browser, resolusi otomatis menyesuaikan ukuran jendela Anda |

4. Klik tombol hijau **Run workflow** untuk mengonfirmasi — desktop cloud mulai booting

### Langkah 3: Dapatkan URL akses

1. Di halaman Actions, klik sesi yang baru Anda mulai (yang paling atas — titik kuning berarti sedang berjalan)
2. Tunggu sekitar 3–5 menit hingga VM selesai menginstal perangkat lunak dan menyiapkan tunnel
3. Klik langkah **启动服务并建立隧道**, buka log-nya, dan gulir ke bawah untuk menemukan URL seperti ini:

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. Salin URL tersebut dan buka di browser Anda (browser bawaan ponsel juga bisa)

### Langkah 4: Terhubung ke desktop

1. Di halaman noVNC yang terbuka, klik **Connect**
2. Masukkan kata sandi VNC yang Anda atur di Langkah 2
3. Anda masuk — nikmati desktop Windows Anda 🎉
4. Resolusi desktop akan otomatis menyesuaikan jendela browser dalam sekitar 10 detik setelah halaman dibuka; mengubah ukuran jendela memicu penyesuaian otomatis (dipilih dari resolusi yang didukung GPU Anda)

> ⌨️ Tekan **Win + Space** untuk beralih metode input antara Sogou Pinyin dan keyboard Inggris.

### Langkah 5: Matikan setelah selesai

- Kembali ke halaman Actions, buka sesi tersebut, dan klik **Cancel run** di kanan atas — VM dihancurkan dan tunnel terputus
- Sesi juga berakhir otomatis setelah durasi yang ditetapkan berlalu, jadi tidak perlu khawatir berjalan selamanya

## ⚠️ Catatan

- **URL berubah setiap sesi**: URL lama berhenti berfungsi begitu sesi sebelumnya berakhir, jadi selalu gunakan URL dari log sesi terbaru
- **Tidak ada yang tersimpan**: setelah VM dihancurkan, file, unduhan, dan status login di desktop semuanya terhapus — pindahkan file penting tepat waktu
- **Aturan kata sandi**: huruf dan angka saja, maksimal 8 karakter — kata sandi yang lebih panjang atau mengandung karakter khusus bisa gagal terhubung (dengan `Authentication failed`)
- **Jangan klik Re-run**: untuk memulai desktop baru, klik **Run workflow** — Re-run menjalankan ulang kode lama
- **Koneksi lambat/ngelag**: tunnel melewati Cloudflare; kecepatan dari Tiongkok daratan tergantung jaringan Anda, tapi masih bisa dipakai
- **Halaman tidak terbuka**: pertama periksa sesi masih berjalan (titik kuning) — jika sudah dibatalkan atau selesai, URL sudah mati

## ❓ FAQ

| Gejala | Penyebab / Solusi |
|------|-----------|
| `loopback connections are not enabled` | Bug versi lama — mulai sesi baru dengan kode terbaru via Run workflow |
| `Server is not configured properly` | Bug versi lama — mulai sesi baru dengan kode terbaru via Run workflow |
| `Authentication failed` | Kata sandi VNC salah, atau kata sandi lebih dari 8 karakter / mengandung karakter khusus |
| 502 / 1033 di halaman | Tunnel belum siap atau terputus — tunggu beberapa menit atau jalankan ulang |
| Resolusi tidak berubah otomatis | Tunggu ~10 detik; pastikan ukuran jendela browser benar-benar berubah; beberapa resolusi non-standar tidak didukung GPU dan yang terdekat dipilih sebagai gantinya |

## 🛠️ Ingin mengubah sendiri?

File workflow ada di `.github/workflows/` (`windows-vnc.yml` untuk edisi standar, `windows-vnc-rustdesk.yml` untuk edisi RustDesk) — Anda bisa mengeditnya langsung di situs GitHub; perubahan berlaku setelah Anda commit.
