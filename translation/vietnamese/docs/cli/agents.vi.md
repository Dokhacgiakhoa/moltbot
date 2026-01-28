---
summary: "Tài liệu tham khảo lệnh `moltbot agents` (Liệt kê/Thêm/Xóa/Thiết lập danh tính Agent)"
read_when:
  - Bạn muốn quản lý nhiều Agent riêng biệt (khác không gian làm việc, khác quyền hạn)
---

# `moltbot agents`

Quản lý các Agent riêng biệt (phân tách về không gian làm việc, xác thực và cơ chế điều phối).

Tài liệu liên quan:
- Điều phối đa Agent: [Multi-Agent Routing](../../concepts/multi-agent.vi.md)
- Không gian làm việc: [Agent workspace](../../concepts/agent-workspace.vi.md)

## Ví dụ sử dụng

```bash
# Xem danh sách các Agent đang có
moltbot agents list

# Thêm một Agent mới tên là "work" với thư mục riêng
moltbot agents add work --workspace ~/clawd-work

# Cập nhật danh tính từ file IDENTITY.md trong thư mục làm việc
moltbot agents set-identity --workspace ~/clawd --from-identity

# Đặt ảnh đại diện cho Agent
moltbot agents set-identity --agent main --avatar avatars/clawd.png

# Xóa một Agent
moltbot agents delete work
```

## Hồ sơ danh tính (Identity)
Mỗi Agent có thể có một file `IDENTITY.md` tại thư mục gốc của mình để định nghĩa:
- **Tên**: Tên hiển thị của bot.
- **Phong cách**: Mô tả ngắn về tính cách.
- **Emoji**: Biểu tượng đại diện.
- **Avatar**: Đường dẫn ảnh đại diện (có thể là đường dẫn máy, URL hoặc base64).

Bạn có thể dùng lệnh `set-identity` để cập nhật các thông tin này vào cấu hình hệ thống, giúp giao diện người dùng hiển thị đúng thông tin của bot.

---
Tài liệu liên quan: [Cơ chế Trí nhớ](../../concepts/memory.vi.md), [Hồ sơ Agent](../../concepts/agent.vi.md).
