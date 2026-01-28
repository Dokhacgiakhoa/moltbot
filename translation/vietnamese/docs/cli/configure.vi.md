---
summary: "Tài liệu tham khảo lệnh `moltbot configure` (Cấu hình tương tác qua các câu hỏi)"
read_when:
  - Bạn muốn điều chỉnh mã xác thực, thiết bị hoặc các cài đặt mặc định của Agent một cách trực quan
---

# `moltbot configure`

Cung cấp giao diện tương tác để thiết lập thông tin đăng nhập, thiết bị và các cấu hình mặc định cho Agent.

**Lưu ý**: Phần **Model** giờ đây cho phép bạn chọn nhiều mô hình cùng lúc để đưa vào "danh sách trắng" (`agents.defaults.models`). Những mô hình này sẽ xuất hiện trong menu chọn của ứng dụng hoặc khi bạn dùng lệnh `/model`.

**Mẹo**: Lệnh `moltbot config` khi chạy không kèm lệnh con cũng sẽ mở trình thuật sĩ tương tự. Nếu muốn chỉnh sửa nhanh không cần tương tác, hãy dùng `moltbot config get|set|unset`.

Tài liệu liên quan:
- Tham khảo cấu hình Gateway: [Cấu hình hệ thống](../gateway/configuration.vi.md)
- Lệnh cấu hình nhanh: [Config](./config.vi.md)

## Ví dụ sử dụng

```bash
moltbot configure
moltbot configure --section models --section channels
```
