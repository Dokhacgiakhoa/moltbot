---
summary: "Bộ điều hợp RPC cho các công cụ CLI bên ngoài (signal-cli, imsg) và các mô hình kết nối Gateway"
read_when:
  - Bạn đang thêm mới hoặc thay đổi tích hợp của các công cụ CLI từ bên ngoài
---

# Bộ điều hợp RPC (RPC adapters)

Moltbot tích hợp với các công cụ dòng lệnh (CLI) bên ngoài thông qua giao thức JSON-RPC. Hiện tại có hai mô hình chính được sử dụng.

## Mô hình A: Chạy như dịch vụ ngầm (HTTP daemon) - Ví dụ: signal-cli
- `signal-cli` chạy như một tiến trình ngầm (daemon) hỗ trợ JSON-RPC qua cổng HTTP.
- Luồng sự kiện sử dụng công nghệ SSE (`/api/v1/events`).
- Kiểm tra sức khỏe qua endpoint: `/api/v1/check`.
- Moltbot tự động quản lý vòng đời khởi động/dừng nếu bạn bật `channels.signal.autoStart=true`.

## Mô hình B: Tiến trình con stdio (stdio child process) - Ví dụ: imsg
- Moltbot khởi chạy lệnh `imsg rpc` như một tiến trình con trực tiếp.
- Dữ liệu JSON-RPC được truyền qua các dòng văn bản (mỗi dòng là một đối tượng JSON) thông qua luồng vào/ra tiêu chuẩn (stdin/stdout).
- Phương thức này không cần mở cổng TCP, không cần chạy dịch vụ ngầm phức tạp.

Các phương thức chính thường dùng:
- `watch.subscribe`: Để nhận thông báo tin nhắn mới.
- `send`: Để gửi tin nhắn đi.
- `chats.list`: Để kiểm tra danh sách hội thoại.

---
Tài liệu liên quan: [Kênh Signal](../channels/signal.vi.md), [Kênh iMessage](../channels/imessage.vi.md).
