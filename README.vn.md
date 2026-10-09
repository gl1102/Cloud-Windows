[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Čeština](README.cs.md) | [Dansk](README.da.md) | [Deutsch](README.de.md) | [Esperanto](README.eo.md) | [فارسی](README.fa.md) | [Suomi](README.fi.md) | [Français](README.fr.md) | [Ελληνικά](README.gr.md) | [Magyar](README.hu.md) | [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [മലയാളം](README.ml.md) | [Nederlands](README.nl.md) | [Norsk](README.no.md) | [Polski](README.pl.md) | [Português](README.ptbr.md) | [Română](README.ro.md) | [Türkçe](README.tr.md) | [Українська](README.ua.md) | [Tiếng Việt](README.vn.md)

# ☁️ Cloud-Windows — Máy tính Windows đám mây miễn phí

Biến máy ảo Windows miễn phí của GitHub Actions thành một máy tính đám mây có thể truy cập từ trình duyệt. Mở một trang web là bạn có ngay một chiếc PC Windows — tắt đi khi dùng xong. Hoàn toàn miễn phí.

## ✨ Tính năng

- 🖥️ Một máy tính Windows đầy đủ, ngay trong trình duyệt của bạn (ứng dụng web noVNC)
- 📐 **Tự động độ phân giải**: sau khi mở trang, độ phân giải màn hình sẽ tự động khớp với kích thước cửa sổ trình duyệt — điện thoại và máy tính đều có kích thước phù hợp; nó cũng tự theo khi bạn đổi kích thước cửa sổ
- 🌐 Truy cập qua Cloudflare Tunnel — không cần IP công cộng, không cần NAT traversal
- ⌨️ Bộ gõ Sogou Pinyin tích hợp sẵn, nhập tiếng Trung hoạt động ngay (nhấn `Win + Space` để chuyển giữa tiếng Trung và tiếng Anh)
- 🖱️ Kết nối từ điện thoại, máy tính bảng hoặc máy tính
- ⏱️ Mỗi lần chạy kéo dài tới ~6 giờ, và bạn có thể hủy bất cứ lúc nào
- 📦 **Phiên bản RustDesk**: còn có một workflow RustDesk tự động tải bản RustDesk mới nhất về ổ D và cài đặt im lặng vào `D:\RustDesk`

## 🚀 Cách dùng (dùng được ngay sau khi fork)

### Bước 1: Fork dự án này

Nhấn nút **Fork** ở góc trên bên phải trang này để sao chép dự án về tài khoản GitHub của bạn. Sau khi fork, bạn sẽ ở trong kho `your-username/Cloud-Windows`.

> 💡 Vì sao phải fork? GitHub Actions chỉ chạy được trên các kho thuộc tài khoản của bạn — fork giúp bạn có quyền chạy nó.

### Bước 2: Khởi động máy tính đám mây

1. Vào trang kho đã fork của bạn và nhấn tab **Actions** ở trên cùng
2. Chọn một workflow ở bên trái (chọn một):
   - **Windows Cloud Desktop**: máy tính đám mây tiêu chuẩn
   - **Windows Cloud Desktop + RustDesk**: bản tiêu chuẩn cộng thêm tự động tải bản RustDesk mới nhất về ổ D và cài đặt im lặng vào `D:\RustDesk` (phiên bản không bị cố định — luôn lấy bản phát hành chính thức mới nhất)
3. Nhấn nút **Run workflow** ở bên phải — một hộp thoại với ba ô nhập hiện ra:

| Tham số | Mô tả |
|------|------|
| VNC password | Mật khẩu bạn sẽ nhập khi kết nối tới máy tính — chỉ chữ cái và số, tối đa 8 ký tự (ví dụ `abc12345`). **Hãy ghi lại** |
| Run duration | Phiên máy tính đám mây này sẽ duy trì trong bao nhiêu phút. Mặc định 300 (5 giờ), tối đa 350 |
| Resolution | Độ phân giải màn hình ban đầu, mặc định 1920x1080; ngay khi bạn mở trang trong trình duyệt, nó sẽ tự điều chỉnh theo kích thước cửa sổ |

4. Nhấn nút xanh **Run workflow** để xác nhận — máy tính đám mây bắt đầu khởi động

### Bước 3: Lấy URL truy cập

1. Trên trang Actions, nhấn vào lần chạy bạn vừa khởi động (cái trên cùng — dấu chấm vàng nghĩa là đang chạy)
2. Đợi khoảng 3–5 phút để máy ảo cài đặt phần mềm và thiết lập tunnel
3. Nhấn vào bước **启动服务并建立隧道**, mở rộng logs và cuộn xuống để tìm một URL như thế này:

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. Sao chép URL và mở trong trình duyệt của bạn (trình duyệt tích hợp của điện thoại hoạt động tốt)

### Bước 4: Kết nối tới máy tính

1. Trên trang noVNC vừa mở, nhấn **Connect**
2. Nhập mật khẩu VNC bạn đã đặt ở Bước 2
3. Bạn đã vào — tận hưởng máy tính Windows của bạn 🎉
4. Độ phân giải màn hình sẽ tự khớp với cửa sổ trình duyệt trong khoảng 10 giây sau khi mở trang; đổi kích thước cửa sổ sẽ kích hoạt tự điều chỉnh lại (chọn từ các độ phân giải mà GPU của bạn hỗ trợ)

> ⌨️ Nhấn **Win + Space** để chuyển phương thức nhập liệu giữa Sogou Pinyin và bàn phím tiếng Anh.

### Bước 5: Tắt khi dùng xong

- Quay lại trang Actions, mở lần chạy đó và nhấn **Cancel run** ở góc trên bên phải — máy ảo bị hủy và tunnel ngừng hoạt động
- Nó cũng tự kết thúc khi hết thời gian đã đặt, nên bạn không lo nó chạy mãi

## ⚠️ Lưu ý

- **URL thay đổi mỗi lần chạy**: URL cũ ngừng hoạt động ngay khi lần chạy trước kết thúc, vì vậy luôn dùng URL từ logs của lần chạy mới nhất
- **Không lưu gì cả**: khi máy ảo bị hủy, các tệp, bản tải xuống và trạng thái đăng nhập trên máy tính đều bị xóa — hãy di chuyển các tệp quan trọng ra kịp thời
- **Quy tắc mật khẩu**: chỉ chữ cái và số, tối đa 8 ký tự — mật khẩu dài hơn hoặc có ký tự đặc biệt có thể không kết nối được (với `Authentication failed`)
- **Đừng nhấn Re-run**: để khởi động máy tính mới, hãy nhấn **Run workflow** — Re-run sẽ chạy lại mã cũ
- **Kết nối chậm/giật**: tunnel đi qua Cloudflare; tốc độ từ Trung Quốc đại lục phụ thuộc vào mạng của bạn, nhưng vẫn dùng được
- **Trang không mở được**: trước tiên kiểm tra xem lần chạy còn đang diễn ra không (dấu chấm vàng) — nếu đã bị hủy hoặc kết thúc, URL đã chết

## ❓ Câu hỏi thường gặp

| Triệu chứng | Nguyên nhân / Cách khắc phục |
|------|-----------|
| `loopback connections are not enabled` | Lỗi của bản cũ — khởi động lần chạy mới với mã mới nhất qua Run workflow |
| `Server is not configured properly` | Lỗi của bản cũ — khởi động lần chạy mới với mã mới nhất qua Run workflow |
| `Authentication failed` | Sai mật khẩu VNC, hoặc mật khẩu dài hơn 8 ký tự / chứa ký tự đặc biệt |
| 502 / 1033 trên trang | Tunnel chưa dựng xong hoặc đã rớt — đợi vài phút hoặc chạy lại |
| Độ phân giải không tự thay đổi | Đợi ~10 giây; đảm bảo cửa sổ trình duyệt thực sự đã đổi kích thước; một số độ phân giải không chuẩn không được GPU hỗ trợ và độ phân giải gần nhất sẽ được chọn |

## 🛠️ Muốn tự tùy chỉnh?

Các tệp workflow nằm trong `.github/workflows/` (`windows-vnc.yml` cho bản tiêu chuẩn, `windows-vnc-rustdesk.yml` cho bản RustDesk) — bạn có thể chỉnh sửa trực tiếp trên trang web GitHub; thay đổi có hiệu lực sau khi commit.
