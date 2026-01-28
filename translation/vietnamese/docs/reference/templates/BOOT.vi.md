---
summary: "Mẫu tệp cấu hình cho các lệnh chạy khi khởi động Bot"
read_when:
  - Bạn đang muốn Bot tự động thực hiện một số tác vụ ngay khi mở máy
---

# BOOT.md

Hãy thêm các chỉ dẫn ngắn gọn và rõ ràng về những việc Moltbot cần làm ngay khi khởi động (yêu cầu bật `hooks.internal.enabled`).

Nếu tác vụ đó cần gửi tin nhắn, hãy sử dụng công cụ gửi tin và sau đó trả lời bằng `NO_REPLY` để tránh làm phiền người dùng với các thông báo rác.

Ví dụ:
- Kiểm tra trạng thái các dịch vụ ngầm.
- Gửi báo cáo tóm tắt công việc của ngày hôm qua.
- Dọn dẹp các tệp tạm trong không gian làm việc.
