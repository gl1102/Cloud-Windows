[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Čeština](README.cs.md) | [Dansk](README.da.md) | [Deutsch](README.de.md) | [Esperanto](README.eo.md) | [فارسی](README.fa.md) | [Suomi](README.fi.md) | [Français](README.fr.md) | [Ελληνικά](README.gr.md) | [Magyar](README.hu.md) | [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [മലയാളം](README.ml.md) | [Nederlands](README.nl.md) | [Norsk](README.no.md) | [Polski](README.pl.md) | [Português](README.ptbr.md) | [Română](README.ro.md) | [Türkçe](README.tr.md) | [Українська](README.ua.md) | [Tiếng Việt](README.vn.md)

# ☁️ Cloud-Windows — Darmowy pulpit Windows w chmurze

Przekształć darmową maszynę wirtualną Windows z GitHub Actions w pulpit chmurowy, do którego masz dostęp z przeglądarki. Otwórz stronę internetową i masz komputer z Windows — wyłącz go, gdy skończysz. Całkowicie za darmo.

## ✨ Funkcje

- 🖥️ Pełny pulpit Windows, bezpośrednio w przeglądarce (klient webowy noVNC)
- 📐 **Automatyczna rozdzielczość**: po otwarciu strony rozdzielczość pulpitu automatycznie dopasowuje się do rozmiaru okna przeglądarki — telefony i komputery otrzymują odpowiedni widok; podąża też za zmianą rozmiaru okna
- 🌐 Dostęp przez Cloudflare Tunnel — bez publicznego IP, bez potrzeby przechodzenia przez NAT
- ⌨️ Wbudowany edytor IME Sogou Pinyin, wprowadzanie chińskich znaków działa od razu (naciśnij `Win + Space`, aby przełączać się między chińskim a angielskim)
- 🖱️ Połącz się z telefonu, tabletu lub komputera
- ⏱️ Każde uruchomienie trwa do ~6 godzin i możesz je anulować w dowolnym momencie
- 📦 **Wersja RustDesk**: dostępny jest też przepływ pracy RustDesk, który automatycznie pobiera najnowszy instalator RustDesk na Pulpit

## 🚀 Użycie (działa od razu po sforkowania)

### Krok 1: Sforkuj ten projekt

Kliknij przycisk **Fork** w prawym górnym rogu tej strony, aby skopiować projekt na własne konto GitHub. Po zrobieniu forka znajdziesz się w repozytorium `your-username/Cloud-Windows`.

> 💡 Po co fork? GitHub Actions może działać tylko w repozytoriach pod Twoim kontem — fork daje Ci uprawnienia do uruchomienia.

### Krok 2: Uruchom pulpit chmurowy

1. Przejdź do strony swojego sforknowanego repozytorium i kliknij zakładkę **Actions** u góry
2. Wybierz przepływ pracy po lewej (wybierz jeden):
   - **Windows Cloud Desktop**: standardowy pulpit chmurowy
   - **Windows Cloud Desktop + RustDesk**: edycja standardowa plus automatyczne pobieranie najnowszego instalatora RustDesk na Pulpit (wersja nie jest wpisana na sztywno — zawsze pobiera najnowsze oficjalne wydanie); gdy potrzebujesz zdalnego sterowania, wystarczy kliknąć dwukrotnie, aby zainstalować
3. Kliknij przycisk **Run workflow** po prawej — wyskoczy okno dialogowe z trzema polami wejściowymi:

| Parametr | Opis |
|------|------|
| VNC password | Hasło, które wpiszesz podczas łączenia z pulpitem — tylko litery i cyfry, maksymalnie 8 znaków (np. `abc12345`). **Zapisz je** |
| Run duration | Ile minut ta sesja pulpitu chmurowego pozostanie aktywna. Domyślnie 300 (5 godzin), maksymalnie 350 |
| Resolution | Początkowa rozdzielczość pulpitu, domyślnie 1920x1080; po otwarciu strony w przeglądarce automatycznie dopasowuje się do rozmiaru okna |

4. Kliknij zielony przycisk **Run workflow**, aby potwierdzić — pulpit chmurowy zaczyna się uruchamiać

### Krok 3: Pobierz adres URL dostępu

1. Na stronie Actions kliknij uruchomienie, które właśnie rozpocząłeś (to najwyższe — żółta kropka oznacza, że działa)
2. Odczekaj około 3–5 minut, aż maszyna wirtualna zainstaluje oprogramowanie i skonfiguruje tunel
3. Kliknij krok **启动服务并建立隧道**, rozwiń logi i przewiń w dół, aby znaleźć adres URL podobny do tego:

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. Skopiuj adres URL i otwórz go w przeglądarce (wbudowana przeglądarka telefonu działa dobrze)

### Krok 4: Połącz się z pulpitem

1. Na otwartej stronie noVNC kliknij **Connect**
2. Wpisz hasło VNC ustawione w kroku 2
3. Jesteś w środku — ciesz się pulpitem Windows 🎉
4. Rozdzielczość pulpitu automatycznie dopasuje się do okna przeglądarki w ciągu około 10 sekund od otwarcia strony; zmiana rozmiaru okna wyzwala automatyczne ponowne dopasowanie (wybrane spośród rozdzielczości obsługiwanych przez Twoją kartę graficzną)

> ⌨️ Naciśnij **Win + Space**, aby przełączyć metodę wprowadzania między Sogou Pinyin a angielską klawiaturą.

### Krok 5: Wyłącz, gdy skończysz

- Wróć na stronę Actions, otwórz uruchomienie i kliknij **Cancel run** w prawym górnym rogu — maszyna wirtualna zostanie zniszczona, a tunel przestanie działać
- Zakończy się również automatycznie po upływie ustawionego czasu, więc nie musisz się martwić, że będzie działać bez końca

## ⚠️ Uwagi

- **Adres URL zmienia się przy każdym uruchomieniu**: stary adres przestaje działać, gdy tylko poprzednie uruchomienie się zakończy, więc zawsze używaj adresu z logów najnowszego uruchomienia
- **Nic nie jest zapisywane**: po zniszczeniu maszyny wirtualnej pliki, pobrane dane i stany logowania na pulpicie zostaną wyczyszczone — przenieś ważne pliki na czas
- **Zasady hasła**: tylko litery i cyfry, maksymalnie 8 znaków — dłuższe hasła lub zawierające znaki specjalne mogą nie połączyć się (z `Authentication failed`)
- **Nie klikaj Re-run**: aby uruchomić nowy pulpit, kliknij **Run workflow** — Re-run odtwarza stary kod
- **Wolne/klatkujące połączenie**: tunel przechodzi przez Cloudflare; prędkości z Chin kontynentalnych zależą od Twojej sieci, ale jest używalne
- **Strona się nie otwiera**: najpierw sprawdź, czy uruchomienie wciąż trwa (żółta kropka) — jeśli zostało anulowane lub zakończone, adres URL jest martwy

## ❓ FAQ

| Objaw | Przyczyna / Rozwiązanie |
|------|-----------|
| `loopback connections are not enabled` | Błąd starej wersji — rozpocznij nowe uruchomienie z najnowszym kodem przez Run workflow |
| `Server is not configured properly` | Błąd starej wersji — rozpocznij nowe uruchomienie z najnowszym kodem przez Run workflow |
| `Authentication failed` | Błędne hasło VNC lub hasło dłuższe niż 8 znaków / zawierające znaki specjalne |
| 502 / 1033 na stronie | Tunel jeszcze nie wstał lub padł — odczekaj kilka minut lub uruchom ponownie |
| Rozdzielczość nie zmieniła się automatycznie | Odczekaj ~10 sekund; upewnij się, że rozmiar okna przeglądarki faktycznie się zmienił; niektóre niestandardowe rozdzielczości nie są obsługiwane przez kartę graficzną i wybierana jest najbliższa |

## 🛠️ Chcesz dostosować samodzielnie?

Pliki przepływów pracy znajdują się w `.github/workflows/` (`windows-vnc.yml` dla edycji standardowej, `windows-vnc-rustdesk.yml` dla edycji RustDesk) — możesz je edytować bezpośrednio na stronie GitHub; zmiany zaczną obowiązywać po commicie.
