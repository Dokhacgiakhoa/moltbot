---
summary: "Tài liệu tham khảo lệnh `moltbot tui` (Giao diện dòng lệnh đồ họa kết nối với Gateway)"
read_when:
  - Bạn muốn trò chuyện với bot trực tiếp trong terminal bằng giao diện trực quan
---

# `moltbot tui`

Mở giao diện người dùng trên Terminal (TUI) để kết nối và trò chuyện với Gateway.

Tài liệu liên quan:
- Hướng dẫn TUI: [Tổng quan giao diện TUI](../../tui.md)

## Ví dụ sử dụng

```bash
# Mở giao diện mặc định (kết nối với Gateway cục bộ)
moltbot tui

# Kết nối tới một Gateway từ xa với mã bảo mật
moltbot tui --url ws://1.2.3.4:18789 --token <mã-của-bạn>

# Mở một phiên trò chuyện cụ thể và gửi phản hồi ngay lập tức
moltbot tui --session main --deliver
```

Giao diện này cực kỳ hữu ích khi bạn đang làm việc trong môi trường SSH hoặc đơn giản là muốn trò chuyện với Agent mà không cần mở trình duyệt web.
