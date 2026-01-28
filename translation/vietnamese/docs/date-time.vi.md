---
summary: "Cách xử lý ngày và giờ trong các tiêu đề tin nhắn, câu lệnh hệ thống, công cụ và kết nối"
---

# Ngày & Giờ (Date & Time)

Moltbot mặc định sử dụng **giờ địa phương của máy chủ Gateway (host-local time)** cho nhãn thời gian truyền tải và chỉ sử dụng **múi giờ của người dùng (user timezone)** trong câu lệnh hệ thống (system prompt).

## Nhãn thời gian tin nhắn (Mặc định là giờ địa phương)

Các tin nhắn đến được bao bọc bởi một nhãn thời gian (độ chính xác đến từng phút):

```
[Provider ... 2026-01-05 16:26 PST] nội dung tin nhắn
```

Bạn có thể thay đổi hành vi này trong cấu hình:

```json
{
  "agents": {
    "defaults": {
      "envelopeTimezone": "local",
      "envelopeTimestamp": "on",
      "envelopeElapsed": "on"
    }
  }
}
```

- `envelopeTimezone`: Có thể chọn là `"utc"`, `"local"`, `"user"` hoặc mã múi giờ IANA (ví dụ: `"Asia/Ho_Chi_Minh"`).
- `envelopeTimestamp`: Bật/tắt việc hiển thị mốc thời gian tuyệt đối.
- `envelopeElapsed`: Bật/tắt việc hiển thị khoảng thời gian đã trôi qua (ví dụ: `+2m`).

## Trong Câu lệnh hệ thống (System Prompt)

Để giữ cho bộ nhớ đệm của câu lệnh (prompt caching) luôn ổn định, trong câu lệnh hệ thống chỉ bao gồm thông tin về **tên múi giờ**, không bao gồm mốc giờ cụ thể:

```
Time zone: Asia/Ho_Chi_Minh
```

Nếu Agent cần biết giờ hiện tại, nó sẽ sử dụng công cụ `session_status` để lấy mốc thời gian chính xác nhất.

## Nhật ký sự kiện hệ thống

Các sự kiện của hệ thống (như việc đổi mô hình AI) chèn vào bối cảnh của Agent cũng sẽ được gắn nhãn thời gian theo giờ địa phương của máy chủ (mặc định):

```
System: [2026-01-12 12:19:17 PST] Model switched.
```

## Định cấu hình múi giờ & định dạng

```json
{
  "agents": {
    "defaults": {
      "userTimezone": "Asia/Ho_Chi_Minh",
      "timeFormat": "auto"
    }
  }
}
```

- `userTimezone`: Múi giờ địa phương của người dùng để Agent hiểu ngữ cảnh thời gian.
- `timeFormat`: Chọn định dạng 12h hoặc 24h. Chế độ `auto` sẽ tự động lấy theo cài đặt của hệ điều hành.

---
Tài liệu liên quan: [Câu lệnh hệ thống](../concepts/system-prompt.vi.md), [Múi giờ](../concepts/timezone.vi.md).
