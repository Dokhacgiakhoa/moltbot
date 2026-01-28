---
summary: "Tài liệu tham khảo lệnh `moltbot config` (Đọc/Ghi/Gỡ bỏ các giá trị cấu hình)"
read_when:
  - Bạn muốn đọc hoặc sửa file cấu hình thông qua các dòng lệnh nhanh
---

# `moltbot config`

Các lệnh hỗ trợ quản lý cấu hình: Đọc (get), Ghi (set), Gỡ bỏ (unset) các giá trị theo đường dẫn. Nếu chạy lệnh này mà không có lệnh con, nó sẽ mở trình thuật sĩ cấu hình tương tác (tương đương với `moltbot configure`).

## Ví dụ sử dụng

```bash
# Đọc đường dẫn trình duyệt
moltbot config get browser.executablePath

# Thiết lập đường dẫn trình duyệt
moltbot config set browser.executablePath "/usr/bin/google-chrome"

# Đặt lịch kiểm tra (heartbeat) mỗi 2 giờ
moltbot config set agents.defaults.heartbeat.every "2h"

# Gỡ bỏ mã API key của công cụ tìm kiếm
moltbot config unset tools.web.search.apiKey
```

## Đường dẫn (Paths)

Bạn có thể sử dụng dấu chấm hoặc dấu ngoặc vuông để truy cập các cấp cấu hình sâu hơn:

```bash
moltbot config get agents.defaults.workspace
moltbot config get agents.list[0].id
```

## Các lưu ý về giá trị
- Các giá trị sẽ được ưu tiên phân tích theo chuẩn JSON5 nếu có thể; nếu không sẽ được coi là chuỗi văn bản thông thường.
- Hãy khởi động lại Gateway sau khi thực hiện các thay đổi để cấu hình mới có hiệu lực.

---
Tài liệu liên quan: [Cấu hình hệ thống](../gateway/configuration.vi.md).
