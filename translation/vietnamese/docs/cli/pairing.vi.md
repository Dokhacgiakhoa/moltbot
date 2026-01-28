---
summary: "Tài liệu tham khảo lệnh `moltbot pairing` (Phê duyệt/Liệt kê các yêu cầu ghép nối)"
read_when:
  - Bạn đang sử dụng chế độ ghép nối tin nhắn trực tiếp DM và cần phê duyệt người gửi
---

# `moltbot pairing`

Phê duyệt hoặc kiểm tra các yêu cầu ghép nối tin nhắn trực tiếp (DM) cho các kênh có hỗ trợ tính năng này (như WhatsApp).

Tài liệu liên quan:
- Quy trình ghép nối: [Pairing](../../start/pairing.vi.md)

## Các lệnh chính

```bash
# Xem danh sách các yêu cầu ghép nối trên WhatsApp
moltbot pairing list whatsapp

# Phê duyệt một mã ghép nối và gửi thông báo cho người gửi
moltbot pairing approve whatsapp <code> --notify
```

Tính năng này giúp bạn kiểm soát ai được phép nhắn tin trực tiếp cho bot của bạn trước khi nó bắt đầu trả lời.
