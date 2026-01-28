---
summary: "Khám phá Gateway qua Bonjour/mDNS: Cách hoạt động, tín hiệu và xử lý lỗi"
read_when:
  - Bạn gặp vấn đề khi kết nối ứng dụng Mac/iOS với Gateway trong mạng nội bộ
---

# Khám phá qua Bonjour / mDNS

Moltbot sử dụng Bonjour (mDNS) như một **tiện ích chỉ dành cho mạng nội bộ (LAN)** để các ứng dụng khách tự động tìm thấy Gateway mà không cần nhập địa chỉ IP thủ công. Đây là một tính năng hỗ trợ và không thay thế cho các kết nối qua SSH hay Tailscale.

## Bonjour diện rộng qua Tailscale

Nếu thiết bị và Gateway nằm ở hai mạng khác nhau, tính năng Bonjour thông thường sẽ không hoạt động. Bạn có thể kích hoạt **DNS-SD diện rộng** thông qua Tailscale để giữ nguyên trải nghiệm tự động kết nối.

Các bước thực hiện:
1. Chạy một máy chủ DNS trên máy chủ Gateway (có thể truy cập qua Tailnet).
2. Công bố các bản ghi DNS-SD cho dịch vụ `_moltbot-gw._tcp`.
3. Cấu hình **DNS phân tách (Split DNS)** trong Tailscale để các thiết bị tự động tìm đến máy chủ DNS này.

Bạn có thể thiết lập nhanh bằng lệnh:
```bash
moltbot dns setup --apply
```

## Các thông tin công bố (TXT records)

Gateway sẽ gửi các tín hiệu nhỏ (không chứa thông tin mật) để ứng dụng khách dễ nhận diện:
- `role=gateway`: Xác định đây là máy chủ Moltbot.
- `displayName`: Tên thân thiện của máy chủ.
- `lanHost`: Tên máy chủ trong mạng `.local`.
- `gatewayPort`: Cổng dịch vụ (Mặc định 18789).

## Kiểm tra trên macOS

Bạn có thể dùng công cụ có sẵn của hệ điều hành để tìm kiếm máy chủ:
```bash
dns-sd -B _moltbot-gw._tcp local.
```

## Các lỗi thường gặp
- **Bonjour không xuyên mạng**: Nếu dùng 4G hoặc mạng khác, hãy dùng Tailscale hoặc SSH.
- **Tên máy chủ quá phức tạp**: Hãy đặt tên máy tính đơn giản, tránh dùng biểu tượng cảm xúc (emoji) vì có thể làm các bộ phân giải tên bị lỗi.
- **Đã tìm thấy nhưng không kết nối được**: Kiểm tra xem tường lửa của hệ điều hành có đang chặn cổng 18789 hay không.

---
Tài liệu liên quan: [Ghép nối thiết bị](./pairing.vi.md), [Sử dụng Tailscale](./tailscale.vi.md).
