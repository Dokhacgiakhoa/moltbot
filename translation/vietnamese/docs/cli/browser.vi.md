---
summary: "Tài liệu tham khảo lệnh `moltbot browser` (Hồ sơ, tab, hành động, chuyển tiếp tiện ích mở rộng)"
read_when:
  - Bạn muốn điều khiển trình duyệt thông qua dòng lệnh hoặc gán quyền cho Agent
  - Bạn muốn sử dụng tiện ích mở rộng Chrome để điều khiển tab hiện tại
---

# `moltbot browser`

Quản lý máy chủ điều khiển trình duyệt của Moltbot và thực hiện các hành động (quản lý tab, chụp ảnh màn hình, điều hướng, click, nhập liệu).

Tài liệu liên quan:
- Công cụ trình duyệt: [Browser tool](../../tools/browser.vi.md)
- Tiện ích Chrome: [Chrome extension](../../tools/chrome-extension.md)

## Các lệnh khởi động nhanh (Cục bộ)

```bash
# Liệt kê các tab đang mở trong Google Chrome
moltbot browser --browser-profile chrome tabs

# Khởi động trình duyệt riêng biệt của Moltbot
moltbot browser --browser-profile clawd start

# Mở một trang web mới
moltbot browser --browser-profile clawd open https://google.com

# Chụp ảnh nội dung trang (snapshot)
moltbot browser --browser-profile clawd snapshot
```

## Các hồ sơ trình duyệt (Profiles)
- `clawd`: Khởi động một phiên Chrome hoàn toàn mới và độc lập (có thư mục dữ liệu riêng). Agent thường dùng hồ sơ này để không ảnh hưởng đến trình duyệt cá nhân của bạn.
- `chrome`: Điều khiển các tab Chrome bạn đang mở sẵn (yêu cầu cài đặt thêm tiện ích mở rộng Chrome relay).

## Điều khiển trình duyệt từ xa (Node host)
Nếu Gateway của bạn chạy trên một máy tính khác với máy tính đang mở trình duyệt, bạn cần chạy một **node host** trên máy tính có trình duyệt. Gateway sẽ đóng vai trò trung gian (proxy) để gửi các lệnh điều khiển tới node đó. Điều này rất hữu ích khi bạn chạy bot trên server nhưng muốn nó điều khiển trình duyệt trên máy tính cá nhân của mình.

---
Tài liệu liên quan: [Cài đặt từ xa](../gateway/remote.vi.md), [Bảo mật](../gateway/security/index.vi.md).
