---
summary: "Tài liệu tham khảo lệnh `moltbot cron` (Lập lịch và chạy các tác vụ chạy ngầm)"
read_when:
  - Bạn muốn lên lịch cho các công việc tự động hoặc đánh thức Agent theo giờ
---

# `moltbot cron`

Quản lý các tác vụ lập lịch (cron jobs) cho trình điều phối của Gateway.

Tài liệu liên quan:
- Các tác vụ Cron: [Lập lịch tự động](../../automation/cron-jobs.vi.md)

**Mẹo**: Sử dụng lệnh `moltbot cron --help` để xem đầy đủ các tùy chọn cấu hình.

## Các thao tác chỉnh sửa phổ biến

Cập nhật cài đặt gửi tin nhắn của một công việc mà không làm thay đổi nội dung thông điệp:
```bash
moltbot cron edit <id-công-việc> --deliver --channel telegram --to "ID_NGƯỜI_NHẬN"
```

Tắt việc tự động gửi tin nhắn cho một công việc cụ thể:
```bash
moltbot cron edit <id-công-việc> --no-deliver
```

Dùng lệnh `list` để xem tất cả các công việc đang có:
```bash
moltbot cron list
```

---
Tài liệu liên quan: [Cron vs Heartbeat](../../automation/cron-vs-heartbeat.md).
