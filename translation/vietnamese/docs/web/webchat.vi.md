---
summary: "Giao diện chat trực tiếp với Gateway qua WebSocket"
read_when:
  - Bạn muốn sử dụng ứng dụng chat chính chủ của Moltbot trên máy Mac hoặc điện thoại
---

# WebChat (Giao diện Chat qua WebSocket)

WebChat là giao diện nhắn tin chính thức của Moltbot, cho phép bạn trò chuyện trực tiếp với Bot mà không cần thông qua các ứng dụng bên thứ ba như WhatsApp hay Telegram.

## Đặc điểm
- Giao diện chat gốc (Native UI) cho iOS và macOS.
- Sử dụng chung quy tắc quản lý phiên và điều hướng như các kênh nhắn tin khác.
- Luôn đảm bảo tốc độ phản hồi nhanh nhất vì kết nối trực tiếp với Gateway.

## Cách sử dụng
1. Khởi động Gateway (`moltbot gateway`).
2. Mở ứng dụng Moltbot trên máy Mac/iPhone hoặc mở tab Chat trong bảng điều khiển web.
3. Đảm bảo bạn đã nhập đúng mã Token hoặc Mật khẩu nếu được yêu cầu.

## Cơ chế hoạt động
- Ứng dụng kết nối tới Gateway qua giao thức WebSocket để gửi và nhận tin nhắn thời gian thực.
- Lịch sử chat được lấy trực tiếp từ Gateway (không lưu tệp rác trên máy khách).
- Nếu Gateway bị tắt, WebChat sẽ chuyển sang chế độ chỉ đọc (Read-only).

---
Tài liệu liên quan: [Giao diện điều khiển](./control-ui.vi.md), [Cấu hình Gateway](../../gateway/configuration.vi.md).
