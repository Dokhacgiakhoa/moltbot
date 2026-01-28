---
summary: "Hướng dẫn xử lý các sự cố thường gặp nhất khi sử dụng Moltbot"
read_when:
  - Hệ thống gặp lỗi, không khởi động được hoặc Agent không trả lời
---

# Xử lý sự cố (Troubleshooting) 🔧

Khi Moltbot hoạt động không như ý muốn, hãy làm theo các bước dưới đây để khắc phục.

## Các lệnh chẩn đoán nhanh

| Lệnh | Ý nghĩa | Khi nào dùng |
|---|---|---|
| `moltbot status` | Tóm tắt nhanh về hệ thống, dịch vụ và trạng thái các kênh. | Khi mới bắt đầu kiểm tra lỗi. |
| `moltbot status --all` | Bản báo cáo đầy đủ nhất, an toàn để gửi cho cộng đồng hỗ trợ vì đã ẩn các bí mật. | Khi bạn cần hỏi trợ giúp từ người khác. |
| `moltbot logs --follow` | Theo dõi nhật ký hệ thống trực tiếp. | Khi muốn biết lý do chính xác tại sao một hành động bị thất bại. |
| `moltbot doctor` | Tự động quét lỗi cấu hình, tệp tin cũ và đề xuất cách sửa. | Khi Gateway không khởi động được hoặc cấu hình bị sai. |

## Các lỗi thường gặp nhất

### 1. "No API key found for provider"
**Lý do:** Bạn chưa cấu hình Khóa API (API Key) cho mô hình đó.
**Cách sửa:** Chạy lệnh `moltbot models auth setup-token --provider <ten-nha-cung-cap>` và dán khóa AI của bạn vào.

### 2. "Device identity required" hoặc lỗi đăng nhập bảng điều khiển
**Lý do:** Trình duyệt của bạn đang truy cập qua chế độ HTTP không an toàn, khiến nó không thể tạo mã định danh thiết bị.
**Cách sửa:**
- Luôn truy cập qua `http://127.0.0.1:18789` (nếu đang ở máy đó).
- Hoặc dùng **Tailscale Serve** để có HTTPS.
- Nếu bắt buộc phải dùng HTTP, hãy bật `gateway.controlUi.allowInsecureAuth: true` trong cấu hình.

### 3. "Address Already in Use" (Cổng bị chiếm dụng)
**Lý do:** Có một bản Moltbot khác hoặc một ứng dụng khác đang dùng cổng 18789.
**Cách sửa:** Chạy `moltbot gateway status` để xem ứng dụng nào đang chiếm cổng, sau đó dừng ứng dụng đó hoặc đổi sang cổng khác bằng lệnh `--port`.

### 4. Bot không trả lời tin nhắn (WhatsApp/Telegram)
**Kiểm tra:**
- Dùng lệnh `moltbot status` để xem bạn có đang trong danh sách `AllowFrom` (Cho phép từ) không.
- Nếu là nhóm chat, hãy chắc chắn bạn đã nhắc tên Bot (@name).
- Xem nhật ký bằng `moltbot logs --follow` để xem Bot có nhận được tin nhắn nhưng bị chặn bởi chính sách bảo mật không.

### 5. Lỗi kết nối WhatsApp
Nếu thấy thông báo bị đăng xuất hoặc không gửi được tin nhắn:
```bash
moltbot channels logout
moltbot channels login --verbose
```
Sau đó quét lại mã QR để đăng nhập lại từ đầu.

---
Tài liệu liên quan: [Nhật ký hệ thống](./logging.vi.md), [Lệnh Doctor](./doctor.vi.md).
