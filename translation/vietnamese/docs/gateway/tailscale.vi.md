---
summary: "Tích hợp Tailscale Serve/Funnel cho bảng điều khiển Gateway"
read_when:
  - Bạn muốn dùng Tailscale để truy cập Moltbot từ xa một cách an toàn và dễ dàng nhất
---

# Tailscale (Bảng điều khiển Gateway)

Moltbot có thể tự động cấu hình tính năng **Tailscale Serve** (trong mạng nội bộ tailnet) hoặc **Funnel** (công khai ra internet) cho bảng điều khiển của nó. Điều này giúp Gateway của bạn vẫn an toàn trên máy chủ nhưng bạn vẫn có thể truy cập qua HTTPS và định danh người dùng.

## Các chế độ hoạt động
- **`serve`**: Chỉ cho phép truy cập từ các thiết bị trong mạng Tailscale của bạn. Gateway vẫn chạy ở `127.0.0.1`.
- **`funnel`**: Mở bảng điều khiển ra internet công cộng qua HTTPS. Moltbot bắt buộc bạn phải đặt mật khẩu trong chế độ này.
- **`off`**: Tắt tính năng tự động cấu hình Tailscale.

## Xác thực tự động (Identity headers)
Khi dùng `mode: "serve"`, nếu bạn bật `gateway.auth.allowTailscale: true`, Moltbot sẽ tự động nhận diện bạn là ai thông qua tài khoản Tailscale. Bạn sẽ không cần phải nhập mã Token hay mật khẩu mỗi khi mở bảng điều khiển.

## Ví dụ cấu hình (Chỉ dùng trong mạng Tailscale)
```json5
{
  "gateway": {
    "bind": "loopback",
    "tailscale": { "mode": "serve" }
  }
}
```
Sau đó bạn có thể truy cập qua địa chỉ: `https://<ten-may-cua-ban>.magictail.net/`

## Lưu ý quan trọng
- Bạn cần cài đặt ứng dụng Tailscale và đăng nhập trước trên máy tính chạy Gateway.
- Chế độ **Funnel** rất nguy hiểm vì nó mở cửa ra internet công cộng, hãy luôn sử dụng mật khẩu cực mạnh.
- Nếu bạn muốn Gateway lắng nghe trực tiếp trên IP của Tailscale mà không cần tính năng Serve (không qua HTTPS), hãy đặt `bind: "tailnet"`.

---
Tài liệu liên quan: [Truy cập từ xa](./remote.vi.md), [Bảng điều khiển Web](../../web/control-ui.vi.md).
