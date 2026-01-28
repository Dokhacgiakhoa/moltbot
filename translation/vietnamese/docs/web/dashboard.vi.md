---
summary: "Truy cập bảng điều khiển Gateway (Control UI) và các chế độ xác thực"
read_when:
  - Bạn muốn thay đổi cách đăng nhập hoặc cách hiển thị bảng điều khiển
---

# Bảng điều khiển (Control UI Dashboard)

Bảng điều khiển là giao diện web của Moltbot, mặc định có thể truy cập tại cổng `18789`.

## Cách mở nhanh
- Nếu chạy trên máy: `http://localhost:18789/`
- Sử dụng lệnh: `moltbot dashboard` (Lệnh này sẽ tự động copy đường dẫn kèm mã đăng nhập an toàn vào bộ nhớ tạm của bạn).

## Bảo mật
Bảng điều khiển là khu vực quản trị viên (có quyền chat, sửa cấu hình, chạy lệnh hệ thống). **Tuyệt đối không để lộ đường dẫn này công khai lên mạng.**

## Xử lý khi gặp lỗi "Unauthorized" (Không có quyền truy cập)
- Chạy lệnh `moltbot dashboard` để lấy một mã thông báo (token) mới.
- Đảm bảo Gateway đang chạy (kiểm tra bằng lệnh `moltbot status`).
- Nếu bạn đang điều khiển máy chủ từ xa, hãy đảm bảo đã thiết lập SSH tunnel hoặc sử dụng Tailscale.

---
Tài liệu liên quan: [Giao diện điều khiển](./control-ui.vi.md), [Truy cập từ xa](../../gateway/remote.vi.md).
