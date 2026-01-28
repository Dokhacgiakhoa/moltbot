---
summary: "Phím tắt khắc phục sự cố đặc thù cho từng kênh (Discord/Telegram/WhatsApp)"
read_when:
  - Kênh đã kết nối nhưng tin nhắn không được gửi/nhận
  - Điều tra lỗi cấu hình kênh (quyền hạn, chế độ riêng tư)
---
# Khắc phục sự cố kênh truyền thông (Channel Troubleshooting)

Trước khi đi sâu vào từng kênh, hãy thử chạy các lệnh chẩn đoán cơ bản sau:

```bash
moltbot doctor
moltbot channels status --probe
```

Lệnh `channels status --probe` sẽ in ra các cảnh báo nếu phát hiện cấu hình sai phổ biến và thực hiện các bước kiểm tra thực tế (thông tin đăng nhập, quyền hạn, tư cách thành viên nhóm).

## Tài liệu sửa lỗi chi tiết cho từng kênh:
- **Discord**: [Sửa lỗi Discord](./discord.vi.md#khắc-phục-sự-cố)
- **Telegram**: [Sửa lỗi Telegram](./telegram.vi.md#khắc-phục-sự-cố)
- **WhatsApp**: [Sửa lỗi WhatsApp](./whatsapp.vi.md#khắc-phục-sự-cố-nhanh)

## Một số lỗi Telegram thường gặp
- **Lỗi Mạng (HttpError)**: Nếu nhật ký ghi `Network request for 'sendMessage' failed`, hãy kiểm tra cấu hình IPv6 của máy chủ. Nếu máy chủ không hỗ trợ IPv6, hãy buộc Telegram sử dụng IPv4 hoặc dùng Proxy.
- **Lỗi `setMyCommands`**: Thường do máy chủ của bạn bị chặn kết nối HTTPS tới `api.telegram.org` (thường gặp ở các VPS bị thắt chặt bảo mật).

---
Tài liệu liên quan: [Khắc phục sự cố Gateway](../gateway/troubleshooting.vi.md), [Nhật ký hệ thống](../gateway/logging.vi.md).
