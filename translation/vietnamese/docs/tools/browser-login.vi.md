---
summary: "Hướng dẫn đăng nhập thủ công để tự động hóa trình duyệt và đăng bài lên X/Twitter"
read_when:
  - Bạn cần đăng nhập vào các trang web để AI tự động thao tác
  - Bạn muốn AI đăng bài lên X/Twitter giúp mình
---
# Đăng nhập trình duyệt & Đăng bài X/Twitter

## Đăng nhập thủ công (Khuyên dùng)
Khi một trang web yêu cầu đăng nhập, bạn nên **tự mình đăng nhập bằng tay** trong hồ sơ trình duyệt của Moltbot (hồ sơ `clawd`).

**Lưu ý quan trọng**: **KHÔNG** cung cấp mật khẩu hoặc thông tin đăng nhập cho AI. Các quy trình đăng nhập tự động của AI thường dễ bị các trang web phát hiện là bot và có thể dẫn đến việc khóa tài khoản của bạn.

## Hồ sơ Chrome nào đang được sử dụng?
Moltbot điều khiển một **hồ sơ Chrome riêng biệt** có tên là `clawd` (thường có giao diện màu cam). Nó hoàn toàn tách biệt với trình duyệt bạn dùng hàng ngày.

Có hai cách để truy cập vào hồ sơ này:
1) **Yêu cầu AI mở trình duyệt**: Sau đó bạn tự thao tác đăng nhập trên cửa sổ đó.
2) **Mở qua dòng lệnh (CLI)**:
   ```bash
   # Khởi động trình duyệt Moltbot
   moltbot browser start
   # Mở trang web cần đăng nhập
   moltbot browser open https://x.com
   ```

## X/Twitter: Quy trình đề xuất
- **Để đọc, tìm kiếm hoặc xem luồng tin nhắn (threads)**: Hãy sử dụng công cụ CLI **bird**. Đây là cách ổn định và không cần mở trình duyệt.
- **Để đăng bài mới**: Sử dụng trình duyệt Moltbot (đã đăng nhập thủ công trước đó).

---
Tài liệu liên quan: [Điều khiển trình duyệt](./browser.vi.md), [Khắc phục lỗi Linux](./browser-linux-troubleshooting.vi.md).
