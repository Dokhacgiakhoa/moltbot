---
summary: "Kiến trúc giao tiếp nội bộ (IPC) của ứng dụng macOS, điều khiển nút mạng và PeekabooBridge"
read_when:
  - Bạn là nhà phát triển đang sửa đổi các cơ chế kết nối giữa các thành phần của ứng dụng Mac
---

# Kiến trúc Giao tiếp Nội bộ (IPC) trên macOS

Ứng dụng Moltbot trên macOS được thiết kế với nhiều thành phần giao tiếp với nhau để đảm bảo tính an toàn và quyền hạn hệ thống ổn định.

## Mô hình hiện tại
- Một **ứng dụng GUI duy nhất** nắm giữ toàn bộ các quyền hạn bảo mật (TCC) như thông báo, ghi màn hình, micro.
- Một **dịch vụ nút mạng (node host service)** chạy ngầm để kết nối với Gateway.
- Hai thành phần này nói chuyện với nhau qua một "đường ống" nội bộ (Unix socket).

## Cách thức hoạt động
1. **Agent** gửi yêu cầu (ví dụ: chụp ảnh màn hình) tới Gateway.
2. **Gateway** chuyển yêu cầu tới Dịch vụ nút mạng qua WebSocket.
3. **Dịch vụ nút mạng** gửi yêu cầu qua đường ống nội bộ tới **Ứng dụng Mac**.
4. **Ứng dụng Mac** thực hiện lệnh (vì nó có quyền truy cập màn hình), hỏi ý kiến người dùng nếu cần, và trả kết quả về.

## Bảo mật đường ống
- Chỉ các tiến trình có cùng một định danh chữ ký (Team ID) mới được phép nói chuyện với nhau.
- Các yêu cầu đều có mã xác thực (Token) và thời gian sống (TTL) ngắn để tránh việc bị giả mạo lệnh điều khiển.

---
Tài liệu liên quan: [Cầu nối Peekaboo](./peekaboo.vi.md), [Ký tên ứng dụng](./signing.vi.md).
