---
summary: "Xử lý múi giờ cho agent, phong bì tin nhắn và lời nhắc"
read_when:
  - Bạn cần hiểu cách dấu thời gian được chuẩn hóa cho mô hình AI
  - Cấu hình múi giờ người dùng cho lời nhắc hệ thống
---
# Múi giờ (Timezones)

Moltbot chuẩn hóa các dấu thời gian để mô hình AI luôn thấy một **thời gian tham chiếu duy nhất**.

## Phong bì tin nhắn (Message envelopes)
Các tin nhắn đến được bao bọc trong một "phong bì" chứa metadata như sau:
```
[Provider ... 2026-01-05 16:26 PST] nội dung tin nhắn
```
Dấu thời gian trong phong bì mặc định là **giờ địa phương của máy chủ Gateway**, với độ chính xác đến từng phút.

Bạn có thể tùy chỉnh qua các cài đặt:
- `envelopeTimezone`: `"local"` (máy chủ), `"utc"`, `"user"` (người dùng), hoặc tên múi giờ IANA (ví dụ: `"Asia/Ho_Chi_Minh"`).
- `envelopeTimestamp`: Bật/tắt hiển thị dấu thời gian tuyệt đối.
- `envelopeElapsed`: Bật/tắt hiển thị hậu tố thời gian trôi qua (ví dụ: `+2m`).

## Múi giờ người dùng trong lời nhắc hệ thống
Hãy thiết lập `agents.defaults.userTimezone` để cho mô hình biết múi giờ địa phương của người dùng. Nếu để trống, Moltbot sẽ tự động lấy theo múi giờ của máy chủ chạy Gateway.

```json5
{
  agents: { defaults: { userTimezone: "Asia/Ho_Chi_Minh" } }
}
```

Lời nhắc hệ thống sẽ bao gồm:
- Mục `Current Date & Time`: Ngày giờ địa phương và múi giờ.
- Định dạng thời gian: 12 giờ hoặc 24 giờ (có thể chỉnh qua `timeFormat`).

---
Tài liệu liên quan: [Lời nhắc hệ thống](./system-prompt.vi.md).
