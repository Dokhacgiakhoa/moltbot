---
summary: "Tài liệu tham khảo lệnh `moltbot approvals` (Quản lý phê duyệt lệnh cho máy chủ hoặc các node)"
read_when:
  - Bạn muốn chỉnh sửa danh sách các lệnh được phép chạy mà không cần sửa file JSON thủ công
---

# `moltbot approvals`

Quản lý việc phê duyệt thực thi lệnh (`exec approvals`) cho **máy tính cục bộ**, **máy chủ gateway**, hoặc một **node từ xa**.

Tài liệu liên quan:
- Cơ chế phê duyệt: [Exec approvals](../../tools/exec-approvals.md)
- Quản lý Node: [Nodes](./nodes.vi.md)

## Các lệnh phổ biến

```bash
# Xem danh sách phê duyệt hiện tại trên máy cục bộ
moltbot approvals get

# Xem danh sách phê duyệt trên một Node cụ thể
moltbot approvals get --node <id-hoac-ten>

# Xem danh sách phê duyệt trên Gateway
moltbot approvals get --gateway
```

## Quản lý danh sách trắng (Allowlist)

Bạn có thể thêm các đường dẫn lệnh cụ thể vào danh sách được phép chạy mà không cần AI phải hỏi lại:

```bash
# Cho phép chạy công cụ tìm kiếm ripgrep (rg)
moltbot approvals allowlist add "~/bin/rg"

# Cho phép chạy lệnh uptime cho tất cả Agent trên một Node cụ thể
moltbot approvals allowlist add --agent "*" --node <id-node> "/usr/bin/uptime"

# Xóa một lệnh khỏi danh sách trắng
moltbot approvals allowlist remove "~/bin/rg"
```

Ghi chú: File phê duyệt thường được lưu tại `~/.clawdbot/exec-approvals.json` trên từng máy tương ứng.

---
Tài liệu liên quan: [Bảo mật](../gateway/security/index.vi.md).
