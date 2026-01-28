---
summary: "Kênh tin nhắn trực tiếp Nostr thông qua tin nhắn mã hóa NIP-04"
read_when:
  - Bạn muốn Moltbot nhận tin nhắn thông qua giao thức phi tập trung Nostr
---
# Nostr

**Trạng thái:** Plugin tùy chọn (mặc định bị tắt).

Nostr là một giao thức phi tập trung cho mạng xã hội. Kênh này cho phép Moltbot nhận và phản hồi các tin nhắn trực tiếp (DM) đã được mã hóa thông qua tiêu chuẩn NIP-04.

## Cài đặt Plugin
Bạn có thể cài đặt plugin Nostr bằng lệnh:
```bash
moltbot plugins install @moltbot/nostr
```

## Thiết lập nhanh
1. **Tạo cặp khóa**: Nếu chưa có, bạn cần một cặp khóa Nostr (Private key và Public key). Bạn có thể dùng công cụ như `nak` để tạo.
2. **Cấu hình**:
   ```json
   {
     "channels": {
       "nostr": {
         "privateKey": "nsec1...", // Khóa bí mật của bot
         "relays": ["wss://relay.damus.io", "wss://nos.lol"] // Danh sách các trạm chuyển tiếp
       }
     }
   }
   ```
3. **Khởi động lại Gateway** để áp dụng thay đổi.

## Quản lý hồ sơ (Profile)
Bạn có thể thiết lập thông tin hiển thị của bot (tên, ảnh đại diện, phần giới thiệu...) trực tiếp trong file cấu hình dưới mục `profile`. Các thông tin này sẽ được xuất bản lên mạng Nostr theo tiêu chuẩn NIP-01.

## Kiểm soát quyền truy cập
- **pairing** (Mặc định): Người lạ nhắn tin sẽ nhận được mã ghép đôi.
- **allowlist**: Chỉ những khóa công khai (pubkey) nằm trong danh sách `allowFrom` mới có thể nhắn tin cho bot.
- **open**: Mọi người đều có thể nhắn tin (Yêu cầu đặt `allowFrom: ["*"]`).

## Các lưu ý về mạng chuyển tiếp (Relays)
- Nên sử dụng từ 2-3 relay để đảm bảo tin nhắn luôn được truyền đi ổn định.
- Tránh dùng quá nhiều relay vì sẽ làm tăng độ trễ và tốn tài nguyên.

## Trạng thái hỗ trợ giao thức
- ✅ **NIP-01**: Các sự kiện cơ bản và hồ sơ người dùng.
- ✅ **NIP-04**: Tin nhắn trực tiếp mã hóa (mặc định).
- 🕒 **NIP-17 / NIP-44**: Đang trong kế hoạch phát triển (tin nhắn dạng Gift-wrap và mã hóa phiên bản mới).

---
Tài liệu liên quan: [Cấu hình hệ thống](../gateway/configuration.vi.md), [Bảo mật](../gateway/security/index.vi.md).
