---
summary: "Quy trình điều khiển Gateway từ xa qua SSH từ ứng dụng macOS"
read_when:
  - Bạn muốn sử dụng MacBook để điều khiển Moltbot chạy trên một máy chủ khác
---

# Điều khiển Từ xa (macOS ⇄ Máy chủ từ xa)

Quy trình này cho phép ứng dụng macOS đóng vai trò là bộ điều khiển từ xa hoàn chỉnh cho một Gateway Moltbot đang chạy trên máy tính khác (máy tính để bàn hoặc máy chủ). 

## Các chế độ hoạt động
- **Cục bộ (Local)**: Mọi thứ chạy ngay trên máy Mac này.
- **Từ xa qua SSH (Mặc định)**: Các lệnh của Moltbot được thực thi trên máy chủ từ xa thông qua kết nối SSH. Ứng dụng Mac sẽ mở một đường truyền SSH an toàn để "bắc cầu" dữ liệu.
- **Từ xa trực tiếp (ws/wss)**: Kết nối trực tiếp tới địa chỉ URL của Gateway (ví dụ qua Tailscale Serve hoặc Proxy) mà không dùng SSH Tunnel.

## Yêu cầu chuẩn bị trên máy chủ từ xa
1. Cài đặt Node.js và CLI `moltbot`.
2. Đảm bảo lệnh `moltbot` có thể chạy được từ bất kỳ đâu (nằm trong PATH).
3. Cho phép đăng nhập SSH bằng chìa khóa (Key auth). Khuyên dùng địa chỉ IP của **Tailscale** để kết nối ổn định.

## Thiết lập trong ứng dụng macOS
1. Mở phần **Settings → General**.
2. Tại mục **Moltbot runs**, chọn **Remote over SSH** và nhập thông tin:
   - **SSH target**: `user@ip-may-chu`.
   - **Identity file**: Đường dẫn tới tệp chìa khóa của bạn (nếu cần).
3. Nhấn **Test remote** để kiểm tra kết nối.

## Xử lý sự cố thường gặp
- **Lỗi exit 127**: Máy chủ từ xa không tìm thấy lệnh `moltbot`. Hãy kiểm tra lại biến môi trường PATH trên máy chủ.
- **Chat không hoạt động**: Kiểm tra xem Gateway trên máy chủ có đang chạy không và cổng 18789 có bị tường lửa chặn không.

---
Tài liệu liên quan: [Bảo mật](../../gateway/security/index.vi.md), [Tích hợp Tailscale](../../gateway/tailscale.vi.md).
