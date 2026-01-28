---
summary: "Tài liệu tham khảo lệnh `moltbot dns` (Công cụ hỗ trợ khám phá mạng diện rộng)"
read_when:
  - Bạn muốn cấu hình hệ thống khám phá Gateway (DNS-SD) thông qua Tailscale và CoreDNS
---

# `moltbot dns`

Các công cụ hỗ trợ thiết lập DNS để tự động tìm kiếm Gateway trong mạng nội bộ và mạng diện rộng (Tailscale + CoreDNS). Hiện tại tính năng này tập trung hỗ trợ cho hệ điều hành macOS sử dụng Homebrew CoreDNS.

Tài liệu liên quan:
- Khám phá mạng: [Discovery](../gateway/discovery.vi.md)
- Cấu hình nâng cao: [Cấu hình hệ thống](../gateway/configuration.vi.md)

## Thiết lập

```bash
# Xem hướng dẫn thiết lập DNS
moltbot dns setup

# Áp dụng các thay đổi cấu hình DNS vào hệ thống
moltbot dns setup --apply
```

Lệnh này giúp bạn thiết lập "Split DNS" cho miền `moltbot.internal`, cho phép các thiết bị trong mạng Tailscale tự động nhận diện và kết nối với Gateway mà không cần nhập địa chỉ IP thủ công.
