---
summary: "Chính sách thử lại cho các cuộc gọi đến nhà cung cấp đầu ra"
read_when:
  - Bạn muốn cập nhật hành vi thử lại hoặc các giá trị mặc định của hệ thống
---

# Chính sách thử lại (Retry policy)

## Mục tiêu
- Thực hiện thử lại cho từng yêu cầu HTTP (gửi tin nhắn, tải ảnh), không phải cho toàn bộ quy trình công việc.
- Đảm bảo thứ tự tin nhắn được giữ nguyên bằng cách chỉ thử lại thao tác hiện tại.
- Tránh việc bị trùng lặp các thao tác quan trọng.

## Các giá trị mặc định
- Số lần thử tối đa: **3 lần**.
- Thời gian chờ giữa các lần: Tăng dần theo lũy kế, tối đa **30 giây**.
- Độ trễ nhiễu (Jitter): **0.1 (10%)** - giúp tránh việc tất cả các yêu cầu bị lỗi cùng gửi lại vào một thời điểm duy nhất.

## Hành vi cụ thể của từng kênh

### WhatsApp / Telegram
- Thử lại khi gặp các lỗi tạm thời như: Lỗi giới hạn băng thông (HTTP 429), lỗi kết nối bị ngắt nửa chừng (reset/closed), hoặc dịch vụ của nhà cung cấp tạm thời không khả dụng.
- Nếu gặp lỗi định dạng Markdown, hệ thống sẽ **không thử lại** mà chuyển sang gửi văn bản thuần túy để đảm bảo người dùng nhận được tin nhắn.

### Discord
- Chủ yếu thử lại khi gặp lỗi HTTP 429 (Rate limit). Hệ thống sẽ tuân thủ thời gian chờ `retry_after` do Discord phản hồi.

## Cấu hình
Bạn có thể tùy chỉnh chính sách này cho từng kênh trong file `moltbot.json`:

```json
{
  "channels": {
    "telegram": {
      "retry": {
        "attempts": 3,
        "minDelayMs": 400,
        "maxDelayMs": 30000
      }
    }
  }
}
```

---
Tài liệu liên quan: [Cấu hình Gateway](../../gateway/configuration.vi.md), [Xử lý lỗi](../../gateway/troubleshooting.vi.md).
