---
summary: "Tài liệu tham khảo lệnh `moltbot system` (Sự kiện hệ thống, Heartbeat, Sự hiện diện)"
read_when:
  - Bạn muốn gửi một sự kiện hệ thống mà không cần tạo lịch trình cron
  - Bạn cần bật hoặc tắt tính năng tự động kiểm tra (heartbeat)
---

# `moltbot system`

Các công cụ hỗ trợ cấp hệ thống cho Gateway: gửi sự kiện hệ thống, điều khiển tính năng heartbeat và xem trạng thái hiện diện của các thành phần.

## Các lệnh phổ biến

```bash
# Gửi một sự kiện hệ thống ngay lập tức tới Agent
moltbot system event --text "Kiểm tra các phản hồi khẩn cấp" --mode now

# Bật lại tính năng heartbeat
moltbot system heartbeat enable

# Xem lần cuối cùng heartbeat hoạt động
moltbot system heartbeat last

# Xem danh sách các thành phần đang hiện diện (nodes, instances...)
moltbot system presence
```

## Giải thích về `system event`
Lệnh này gửi một thông báo hệ thống vào phiên làm việc **chính**. Ở lượt xử lý tiếp theo, thông báo này sẽ xuất hiện dưới dạng một dòng `System:` trong ngữ cảnh gửi cho AI. 
- Sử dụng `--mode now` để kích hoạt AI xử lý ngay lập tức.
- Sử dụng `next-heartbeat` (mặc định) để đợi đến lần kiểm tra định kỳ tiếp theo.

## Ghi chú
- Các lệnh này yêu cầu Gateway phải đang chạy và có thể kết nối được.
- Các sự kiện hệ thống chỉ mang tính chất tạm thời và sẽ mất đi nếu bạn khởi động lại Gateway.

---
Tài liệu liên quan: [Cổng kết nối Gateway](./gateway.vi.md), [Xử lý Heartbeat](../gateway/heartbeat.vi.md).
