[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Čeština](README.cs.md) | [Dansk](README.da.md) | [Deutsch](README.de.md) | [Esperanto](README.eo.md) | [فارسی](README.fa.md) | [Suomi](README.fi.md) | [Français](README.fr.md) | [Ελληνικά](README.gr.md) | [Magyar](README.hu.md) | [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [മലയാളം](README.ml.md) | [Nederlands](README.nl.md) | [Norsk](README.no.md) | [Polski](README.pl.md) | [Português](README.ptbr.md) | [Română](README.ro.md) | [Türkçe](README.tr.md) | [Українська](README.ua.md) | [Tiếng Việt](README.vn.md)

# ☁️ Cloud-Windows — Ücretsiz Bulut Windows Masaüstü

Ücretsiz GitHub Actions Windows sanal makinesini, tarayıcıdan erişebileceğiniz bir bulut masaüstüne dönüştürün. Bir web sayfası açın ve bir Windows PC'niz olsun — işiniz bitince kapatın. Tamamen ücretsiz.

## ✨ Özellikler

- 🖥️ Tam bir Windows masaüstü, doğrudan tarayıcınızda (noVNC web istemcisi)
- 📐 **Otomatik çözünürlük**: sayfayı açtıktan sonra masaüstü çözünürlüğü tarayıcı pencerenizin boyutuna otomatik olarak uyar — telefonlar ve PC'ler her biri doğru uyumu alır; pencereyi yeniden boyutlandırdığınızda da takip eder
- 🌐 Cloudflare Tunnel ile erişim — genel IP yok, NAT geçişine gerek yok
- ⌨️ Yerleşik Sogou Pinyin IME, Çince girişi kutudan çıktığı gibi çalışır (`Win + Space` tuşlarıyla Çince ve İngilizce arasında geçiş yapın)
- 🖱️ Telefonunuzdan, tabletinizden veya bilgisayarınızdan bağlanın
- ⏱️ Her çalıştırma ~6 saate kadar sürer ve istediğiniz zaman iptal edebilirsiniz
- 📦 **RustDesk sürümü**: en son RustDesk'i otomatik olarak D sürücüsüne indirip `D:\RustDesk` konumuna sessizce kuran bir RustDesk iş akışı da var

## 🚀 Kullanım (fork'tan hemen sonra çalışır)

### Adım 1: Bu projeyi fork'layın

Projeyi kendi GitHub hesabınıza kopyalamak için bu sayfanın sağ üst köşesindeki **Fork** düğmesine tıklayın. Fork'ladıktan sonra `your-username/Cloud-Windows` deposuna ulaşırsınız.

> 💡 Neden fork? GitHub Actions yalnızca kendi hesabınızdaki depolarda çalışabilir — fork, onu çalıştırma izni verir.

### Adım 2: Bulut masaüstünü başlatın

1. Fork'ladığınız deponun sayfasına gidin ve üstteki **Actions** sekmesine tıklayın
2. Soldan bir iş akışı seçin (birini seçin):
   - **Windows Cloud Desktop**: standart bulut masaüstü
   - **Windows Cloud Desktop + RustDesk**: standart sürüm artı en son RustDesk'in D sürücüsüne otomatik indirilmesi ve `D:\RustDesk` konumuna sessiz kurulumu (sürüm sabit kodlanmamış — her zaman en son resmi sürümü alır)
3. Sağdaki **Run workflow** düğmesine tıklayın — üç giriş alanlı bir iletişim kutusu açılır:

| Parametre | Açıklama |
|------|------|
| VNC password | Masaüstüne bağlanırken gireceğiniz parola — yalnızca harf ve rakam, en fazla 8 karakter (örn. `abc12345`). **Not edin** |
| Run duration | Bu bulut masaüstü oturumunun kaç dakika canlı kalacağı. Varsayılan 300 (5 saat), en fazla 350 |
| Resolution | İlk masaüstü çözünürlüğü, varsayılan 1920x1080; sayfayı tarayıcıda açtığınızda pencere boyutunuza otomatik uyarlanır |

4. Onaylamak için yeşil **Run workflow** düğmesine tıklayın — bulut masaüstü açılmaya başlar

### Adım 3: Erişim URL'sini alın

1. Actions sayfasında az önce başlattığınız çalıştırmaya tıklayın (en üstteki — sarı nokta çalışıyor demek)
2. Sanal makinenin yazılımı kurması ve tüneli yapılandırması için yaklaşık 3–5 dakika bekleyin
3. **启动服务并建立隧道** adımına tıklayın, günlükleri genişletin ve aşağı kaydırarak şuna benzer bir URL bulun:

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. URL'yi kopyalayın ve tarayıcınızda açın (telefonunuzun yerleşik tarayıcısı gayet iyi çalışır)

### Adım 4: Masaüstüne bağlanın

1. Açılan noVNC sayfasında **Connect**'e tıklayın
2. Adım 2'de belirlediğiniz VNC parolasını girin
3. İçeridesiniz — Windows masaüstünüzün keyfini çıkarın 🎉
4. Masaüstü çözünürlüğü, sayfayı açtıktan yaklaşık 10 saniye içinde tarayıcı pencerenize otomatik uyum sağlar; pencereyi yeniden boyutlandırmak otomatik yeniden uyumu tetikler (GPU'nuzun desteklediği çözünürlükler arasından seçilir)

> ⌨️ Sogou Pinyin ile İngilizce klavye arasında giriş yöntemini değiştirmek için **Win + Space** tuşlarına basın.

### Adım 5: İşiniz bitince kapatın

- Actions sayfasına dönün, çalıştırmayı açın ve sağ üstteki **Cancel run** düğmesine tıklayın — sanal makine yok edilir ve tünel ölür
- Belirlenen süre dolduğunda da otomatik olarak sona erer, sonsuza kadar çalışacağından endişelenmeyin

## ⚠️ Notlar

- **URL her çalıştırmada değişir**: önceki çalıştırma biter bitmez eski URL çalışmayı bırakır, bu nedenle her zaman en son çalıştırmanın günlüklerindeki URL'yi kullanın
- **Hiçbir şey kaydedilmez**: sanal makine yok edildiğinde masaüstündeki dosyalar, indirmeler ve oturum açma durumları silinir — önemli dosyaları zamanında taşıyın
- **Parola kuralları**: yalnızca harf ve rakam, en fazla 8 karakter — daha uzun parolalar veya özel karakter içerenler bağlanamayabilir (`Authentication failed` ile)
- **Re-run'a tıklamayın**: yeni bir masaüstü başlatmak için **Run workflow**'a tıklayın — Re-run eski kodu tekrar oynatır
- **Yavaş/takılan bağlantı**: tünel Cloudflare üzerinden geçiyor; Çin ana karasından hızlar ağınıza bağlı, ancak kullanılabilir
- **Sayfa açılmıyor**: önce çalıştırmanın hâlâ devam edip etmediğini kontrol edin (sarı nokta) — iptal edildiyse veya bittiyse URL ölmüştür

## ❓ SSS

| Belirti | Nedeni / Çözümü |
|------|-----------|
| `loopback connections are not enabled` | Eski sürüm hatası — Run workflow ile en son kodla yeni bir çalıştırma başlatın |
| `Server is not configured properly` | Eski sürüm hatası — Run workflow ile en son kodla yeni bir çalıştırma başlatın |
| `Authentication failed` | Yanlış VNC parolası veya parola 8 karakterden uzun / özel karakter içeriyor |
| Sayfada 502 / 1033 | Tünel henüz açılmadı veya düştü — birkaç dakika bekleyin veya yeniden çalıştırın |
| Çözünürlük otomatik değişmedi | ~10 saniye bekleyin; tarayıcı penceresinin gerçekten boyut değiştirdiğinden emin olun; bazı standart dışı çözünürlükler GPU tarafından desteklenmiyor ve en yakın olanı seçiliyor |

## 🛠️ Kendiniz düzenlemek ister misiniz?

İş akışı dosyaları `.github/workflows/` altında (`windows-vnc.yml` standart sürüm için, `windows-vnc-rustdesk.yml` RustDesk sürümü için) — bunları doğrudan GitHub web sitesinde düzenleyebilirsiniz; değişiklikler commit'ten sonra geçerli olur.
