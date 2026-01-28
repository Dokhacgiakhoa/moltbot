---
summary: "Tài liệu tham khảo lệnh `moltbot nodes` (Liệt kê/Trạng thái/Phê duyệt/Gửi lệnh tới Node)"
read_when:
  - Bạn đang quản lý các thiết bị đã ghép nối (camera, máy trạm, màn hình)
  - Bạn cần phê duyệt yêu cầu kết nối hoặc gửi lệnh điều khiển tới một node cụ thể
---

# `moltbot nodes`

Quản lý các node (thiết bị) đã ghép nối và kích hoạt các khả năng đặc nhiệm của chúng.

Tài liệu liên quan:
- Tổng quan về Nodes: [Danh sách Node](../../nodes.vi.md)
- Camera: [Camera nodes](../../nodes/camera.vi.md)

## Các lệnh phổ biến

```bash
# Xem danh sách tất cả các node
moltbot nodes list

# Xem các yêu cầu ghép nối đang chờ xử lý
moltbot nodes pending

# Phê duyệt một thiết bị mới kết nối
moltbot nodes approve <ID_yeu_cau>

# Kiểm tra trạng thái kết nối thực tế
moltbot nodes status --connected
```

## Gửi lệnh tới Node (Invoke / Run)

Bạn có thể gửi lệnh trực tiếp tới một máy tính khác đã kết nối node host:

```bash
# Gửi lệnh dạng thấp (RPC)
moltbot nodes invoke --node <id-hoac-ten> --command system.run --params '{"command": "ls"}'

# Gửi lệnh trực tiếp
moltbot nodes run --node <id-hoac-ten> "git status"
```

Lưu ý: Việc chạy lệnh từ xa vẫn tuân thủ các quy tắc bảo mật và phê duyệt lệnh (`exec approvals`) giống như khi chạy cục bộ.

---
Tài liệu liên quan: [Cơ chế Phê duyệt lệnh](../../tools/exec-approvals.md), [Bảo mật](../gateway/security/index.vi.md).
