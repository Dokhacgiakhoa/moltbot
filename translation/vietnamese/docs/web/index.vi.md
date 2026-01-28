---
summary: "Các bề mặt giao diện web của Gateway: Control UI, các chế độ kết nối và bảo mật"
read_when:
  - Bạn muốn tìm hiểu cách Moltbot hiển thị trên trình duyệt hoặc qua mạng
---

# Web (Gateway)

Gateway của Moltbot tích hợp sẵn một **giao diện điều khiển (Control UI)** chạy trên trình duyệt web tại cùng một cổng với dịch vụ WebSocket:

- Mặc định: `http://<ip-cua-ban>:18789/`

Trang này tập trung vào các chế độ kết nối mạng và các lưu ý về bảo mật khi sử dụng giao diện web.

## Webhooks
Khi được bật (`hooks.enabled=true`), Gateway cũng hỗ trợ nhận dữ liệu từ các dịch vụ bên ngoài (như GitHub, Stripe) thông qua cùng một máy chủ HTTP này.

## Các chế độ kết nối mạng

### 1. Kết nối nội bộ (Loopback)
Mặc định Bot chỉ lắng nghe các kết nối từ chính máy tính đang chạy nó. Đây là chế độ an toàn nhất.

### 2. Sử dụng Tailscale (Khuyên dùng)
Cho phép bạn truy cập bảng điều khiển an toàn từ điện thoại hoặc máy tính khác mà không cần mở cổng modem.
Cấu hình mẫu:
```json5
{
  "gateway": {
    "bind": "loopback",
    "tailscale": { "mode": "serve" }
  }
}
```

### 3. Kết nối công khai (Funnel)
Cho phép truy cập bảng điều khiển từ internet thông qua tính năng Funnel của Tailscale (yêu cầu bảo mật bằng mật khẩu).

## Lưu ý về bảo mật
- Moltbot luôn yêu cầu xác thực bằng Mã Token hoặc Mật khẩu khi truy cập web.
- Mã Token được sinh ra tự động trong quá trình cài đặt ban đầu.
- Giao diện web này có quyền hạn rất cao (có thể đọc tin nhắn, sửa cài đặt), nên hãy cẩn thận khi chia sẻ quyền truy cập.

---
Tài liệu liên quan: [Bảng điều khiển](./dashboard.vi.md), [Bảo mật Gateway](../../gateway/security.vi.md).
