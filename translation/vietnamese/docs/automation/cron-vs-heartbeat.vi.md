---
summary: "Hướng dẫn lựa chọn giữa Heartbeat và Cron cho các tác vụ tự động"
read_when:
  - Bạn đang thiết lập các công việc lặp lại (như kiểm tra email, nhắc việc)
  - Bạn muốn tiết kiệm token khi chạy các tác vụ định kỳ
---

# Cron vs Heartbeat: Nên chọn cái nào?

Cả Heartbeat và Cron đều cho phép bạn chạy các tác vụ theo lịch trình. Hướng dẫn này sẽ giúp bạn chọn công cụ phù hợp nhất.

## Bảng so sánh nhanh

| Tình huống sử dụng | Công cụ khuyên dùng | Tại sao? |
|----------|-------------|-----|
| Kiểm tra email mỗi 30 phút | **Heartbeat** | Gộp chung được với các kiểm tra khác, tiết kiệm token. |
| Gửi báo cáo đúng 9:00 sáng | **Cron (isolated)** | Độ chính xác về thời gian rất cao. |
| Theo dõi lịch trình cá nhân | **Heartbeat** | Phù hợp để duy trì nhận thức liên tục. |
| Phân tích dữ liệu nặng hàng tuần | **Cron (isolated)** | Tác vụ độc lập, có thể dùng mô hình mạnh hơn. |
| Nhắc tôi sau 20 phút | **Cron (main, --at)** | Nhắc việc một lần với thời gian chính xác. |

## Heartbeat: Nhận thức liên tục
Heartbeat chạy trong **phiên chính (main)** theo một khoảng thời gian đều đặn (mặc định 30 phút). Nó được thiết kế để Agent tự kiểm tra mọi thứ và báo cáo những gì quan trọng.

- **Ưu điểm**: Gộp nhiều việc vào một lần chạy (Check email, check lịch, check thời tiết...). Agent có đầy đủ ngữ cảnh của cuộc trò chuyện gần đây nên phản hồi rất tự nhiên.
- **Tiết kiệm**: Nếu không có gì mới, Agent chỉ trả về `HEARTBEAT_OK` và không tốn phí gửi tin nhắn.

## Cron: Lập lịch chính xác
Cron chạy tại **thời điểm chính xác** (ví dụ: đúng 07:00:00) và có thể chạy trong một phiên cô lập để không làm loãng lịch sử chat chính của bạn.

- **Ưu điểm**: Hỗ trợ biểu thức cron phức tạp (0 7 * * *), hỗ trợ múi giờ. Cho phép đổi mô hình AI tùy theo công việc (ví dụ dùng mô hình rẻ tiền để tóm tắt, dùng mô hình xịn để phân tích).
- **Cách dùng**: Phù hợp cho "Morning Briefing" hoặc các lời nhắc một lần (`--at "2h"`).

## Lời khuyên chung: Hãy kết hợp cả hai
Một hệ thống tự động hiệu quả nhất nên dùng cả hai:
1. **Heartbeat**: Để theo dõi routine hàng ngày (vừa gộp việc, vừa rẻ).
2. **Cron**: Để đặt lịch cho những việc quan trọng cần đúng giờ hoặc cần "sức mạnh" của các mô hình AI lớn.

---
Tài liệu liên quan: [Cấu hình Heartbeat](../gateway/heartbeat.vi.md), [Hướng dẫn Cron](./cron-jobs.vi.md).
