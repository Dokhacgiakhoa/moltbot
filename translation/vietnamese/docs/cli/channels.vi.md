---
summary: "Tài liệu tham khảo lệnh `moltbot channels` (Tài khoản, Trạng thái, Đăng nhập và Nhật ký kênh)"
read_when:
  - Bạn muốn thêm/xóa các tài khoản chat (WhatsApp, Telegram, Discord...)
  - Bạn muốn kiểm tra tình trạng kết nối của các kênh
---

# `moltbot channels`

Quản lý các tài khoản kênh chat và trạng thái hoạt động của chúng trên Gateway.

Tài liệu liên quan:
- Hướng dẫn các kênh: [Danh mục kênh](../channels/index.vi.md)
- Cấu hình hệ thống: [Cấu hình Gateway](../gateway/configuration.vi.md)

## Các lệnh phổ biến

```bash
# Liệt kê các kênh đã cấu hình
moltbot channels list

# Kiểm tra sức khỏe kết nối của các kênh
moltbot channels status

# Xem nhật ký (logs) riêng của các kênh chat
moltbot channels logs --channel all
```

## Thêm hoặc xóa tài khoản
Để thêm một bot mới, bạn có thể truyền trực tiếp mã token qua dòng lệnh:
```bash
# Thêm Telegram
moltbot channels add --channel telegram --token <mã-token-bot>

# Xóa một kênh
moltbot channels remove --channel telegram --delete
```

**Mẹo**: Sử dụng lệnh `moltbot channels add --help` để xem danh sách các cờ cấu hình riêng cho từng loại kênh (WhatsApp cần quét mã QR, Discord cần token app, v.v.).

## Đăng nhập tương tác
Đối với WhatsApp Web, bạn cần quét mã QR để đăng nhập:
```bash
moltbot channels login --channel whatsapp
```

## Khắc phục sự cố
- Sử dụng lệnh `moltbot status --deep` để kiểm tra toàn diện.
- Sử dụng `moltbot doctor` để được hướng dẫn sửa các lỗi cấu hình phổ biến.
- Nếu `channels list` báo lỗi 403, hãy kiểm tra lại mã xác thực hoặc hạn mức của tài khoản AI.

---
Tài liệu liên quan: [Xác thực OAuth](../../concepts/oauth.vi.md), [Sửa lỗi kết nối](../gateway/troubleshooting.vi.md).
