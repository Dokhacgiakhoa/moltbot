---
summary: "Tích hợp PeekabooBridge để tự động hóa giao diện người dùng trên macOS"
read_when:
  - Bạn đang sử dụng công cụ Peekaboo để điều khiển UI máy Mac thông qua Moltbot
---

# Cầu nối Peekaboo (Tự động hóa UI trên macOS)

Moltbot có thể đóng vai trò là một máy chủ trung gian cho **PeekabooBridge**. Điều này cho phép các công cụ dòng lệnh `peekaboo` có thể thực hiện các thao tác tự động hóa trên màn hình máy Mac của bạn bằng cách tận dụng các quyền hạn bảo mật mà bạn đã cấp cho Moltbot.app.

## Cách kích hoạt
Trong ứng dụng macOS:
- Vào phần Settings → Bật **Enable Peekaboo Bridge**.

Khi được bật, Moltbot sẽ khởi động một cổng kết nối nội bộ (UNIX socket). Các ứng dụng tự động hóa sẽ gửi lệnh qua cổng này để chụp ảnh màn hình hoặc giả lập thao tác chuột/phím.

## Thứ tự tìm kiếm máy chủ
Các ứng dụng điều khiển UI thường tìm máy chủ theo thứ tự:
1. Peekaboo.app (Giao diện đầy đủ).
2. Claude.app (Nếu có cài đặt).
3. **Moltbot.app** (Máy chủ trung gian).

## Bảo mật & Quyền hạn
- Cầu nối này kiểm tra **chữ ký mã nguồn** của bên gọi lệnh; chỉ những ứng dụng nằm trong danh sách an toàn (như Peekaboo hoặc chính Moltbot) mới được phép điều khiển.
- Nếu bạn chưa cấp quyền "Ghi màn hình" hoặc "Trợ năng" cho Moltbot, cầu nối sẽ trả về thông báo lỗi thay vì thực hiện lệnh.

---
Tài liệu liên quan: [Quyền hạn trên macOS](./permissions.vi.md), [Cấu hình Gateway](../../gateway/configuration.vi.md).
