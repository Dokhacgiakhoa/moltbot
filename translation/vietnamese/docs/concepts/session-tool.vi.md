---
summary: "Bộ công cụ quản lý phiên: liệt kê, lấy lịch sử và gửi tin nhắn xuyên phiên"
read_when:
  - Thêm hoặc chỉnh sửa các công cụ liên quan đến phiên làm việc
---
# Công cụ phiên làm việc (Session Tools)

Mục tiêu: Cung cấp một bộ công cụ nhỏ, an toàn để agent có thể quản lý các phiên làm việc, xem lịch sử và gửi tin nhắn tới các phiên khác.

## Danh sách công cụ
- `sessions_list`: Liệt kê các phiên làm việc.
- `sessions_history`: Lấy lịch sử chat của một phiên.
- `sessions_send`: Gửi một tin nhắn vào một phiên khác.
- `sessions_spawn`: Khởi tạo một phiên chạy agent phụ (sub-agent) độc lập.

## Các loại phiên chính
- `main`: Phiên chat trực tiếp chính của agent.
- `group`: Các phiên chat nhóm (WhatsApp/Telegram/Discord...).
- `cron`: Các phiên chạy định kỳ.
- `hook`: Các phiên kích hoạt qua Webhook.
- `node`: Các phiên kết nối từ các nút (nodes).

## Tính năng sessions_send (Gửi tin nhắn xuyên phiên)
Cho phép agent hiện tại gửi một yêu cầu tới một agent/phiên khác. Moltbot sẽ thực hiện một **vòng lặp trả lời ngược lại (reply-back loop)**:
- Cho phép hai agent "nói chuyện" với nhau qua lại (tối đa 5 lượt ping-pong).
- Sau khi kết thúc hội thoại giữa hai agent, kết quả cuối cùng sẽ được thông báo (announce) lại cho người dùng tại kênh chat gốc.

## Tính năng sessions_spawn (Agent phụ)
Khởi tạo một lượt chạy agent phụ trong một phiên cô lập:
- Agent phụ mặc định có đầy đủ công cụ nhưng **không có công cụ phiên** (ngăn chặn việc khởi tạo vô hạn).
- Kết quả chạy của agent phụ sẽ được tự động báo cáo lại kênh chat của người dùng sau khi hoàn thành.
- Các phiên agent phụ sẽ được tự động lưu trữ (archive) sau 60 phút không hoạt động.

---
Tài liệu liên quan: [Quản lý phiên](./session.vi.md), [Subagents](../tools/subagents.vi.md).
