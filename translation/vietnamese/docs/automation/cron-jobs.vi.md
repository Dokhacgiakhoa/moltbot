---
summary: "Các công việc định kỳ (Cron jobs) và đánh thức cho bộ lập lịch của Gateway"
read_when:
  - Bạn muốn lập lịch chạy các công việc ngầm hoặc nhắc việc
  - Bạn đang phân vân giữa việc dùng Heartbeat hay Cron cho các tác vụ định kỳ
---

# Công việc định kỳ (Cron jobs)

Moltbot tích hợp sẵn một bộ lập lịch bên trong Gateway. Nó cho phép lưu trữ các công việc, đánh thức Agent vào đúng thời điểm và có thể gửi kết quả trực tiếp về cửa sổ chat.

## Tóm tắt nhanh
- **Vị trí chạy**: Chạy **bên trong Gateway** (không phải bên trong mô hình AI).
- **Lưu trữ**: Các công việc được lưu tại `~/.clawdbot/cron/`, không bị mất khi khởi động lại.
- **Hai kiểu thực thi**:
  - **Phiên chính (Main)**: Thêm một sự kiện vào hệ thống, Agent sẽ xử lý ở lượt Heartbeat tiếp theo.
  - **Cô lập (Isolated)**: Chạy một lượt Agent riêng biểu trong phiên `cron:<jobId>`, có thể gửi kết quả ra ngoài.

## Lựa chọn lịch trình
- **Nhắc việc một lần**: Dùng `--at` (ví dụ: `20m` hoặc một mốc thời gian ISO).
- **Lặp lại**: Dùng `--every` (khoảng thời gian) hoặc biểu thức `--cron` chuẩn 5 trường.

## Lựa chọn nơi chạy
- `--session main`: Chạy kèm với luồng suy nghĩ bình thường của Bot (Heartbeat).
- `--session isolated`: Chạy riêng biệt để không làm phiền cửa sổ chat chính, phù hợp cho các tác vụ "dọn dẹp" hoặc phân tích nặng.

## Ví dụ lệnh CLI

**1. Nhắc việc một lần sau 20 phút (Phiên chính):**
```bash
moltbot cron add --name "Nhắc họp" --at "20m" --session main --system-event "Nhắc nhở: Cuộc họp sẽ bắt đầu sau 10 phút." --wake now
```

**2. Báo cáo buổi sáng hàng ngày lúc 7:00 (Gửi về WhatsApp):**
```bash
moltbot cron add --name "Chào buổi sáng" --cron "0 7 * * *" --tz "Asia/Ho_Chi_Minh" --session isolated --message "Tóm tắt email và lịch trình hôm nay cho tôi." --deliver --channel whatsapp --to "+84..."
```

**3. Phân tích sâu hàng tuần (Dùng mô hình mạnh nhất):**
```bash
moltbot cron add --name "Phân tích tuần" --cron "0 9 * * 1" --session isolated --message "Phân tích tiến độ dự án tuần qua." --model opus --thinking high
```

## Kiểm tra và Quản lý
- Liệt kê các công việc: `moltbot cron list`
- Xem lịch sử chạy: `moltbot cron runs --id <jobId>`
- Chạy thử ngay lập tức: `moltbot cron run <jobId> --force`

---
Tài liệu liên quan: [So sánh Cron vs Heartbeat](./cron-vs-heartbeat.vi.md), [Cấu hình Heartbeat](../gateway/heartbeat.vi.md).
