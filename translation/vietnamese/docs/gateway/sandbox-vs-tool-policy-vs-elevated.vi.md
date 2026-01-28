---
summary: "Tìm hiểu tại sao một công cụ AI bị chặn: Do môi trường Sandbox, do chính sách cho phép hay do quyền ưu tiên"
read_when:
  - Bạn thấy thông báo lỗi một công cụ bị chặn hoặc bị từ chối thực hiện
---

# So sánh: Sandbox, Chính sách công cụ và Quyền ưu tiên

Moltbot sử dụng ba lớp bảo vệ khác nhau để điều khiển hành vi của Agent:

1. **Sandbox (Cô lập)**: Quyết định công cụ sẽ chạy **ở đâu** (Trong Docker hay trực tiếp trên máy).
2. **Chính sách công cụ (Tool Policy)**: Quyết định công cụ nào **được phép tồn tại** và được dùng.
3. **Quyền ưu tiên (Elevated)**: Một "lối thoát" riêng cho phép một lệnh vốn bị cô lập được chạy trực tiếp trên máy chủ trong các trường hợp đặc biệt.

## Cách kiểm tra nhanh
Nếu bạn không hiểu tại sao một lệnh bị chặn, hãy dùng Terminal và gõ:
```bash
moltbot sandbox explain
```
Hệ thống sẽ giải thích cặn kẽ: Agent nào đang chạy, nó đang ở trong hay ngoài Sandbox, và quy tắc nào đang chặn nó.

## Quy tắc của Chính sách công cụ
- **Cấm (Deny) luôn thắng**: Nếu bạn đã liệt kê một công cụ vào danh sách cấm, không có cách nào Agent có thể gọi nó.
- **Danh sách trắng (Allow)**: Nếu bạn khai báo danh sách này, mọi công cụ không nằm trong đó sẽ bị coi là bị cấm.
- **Nhóm công cụ**: Bạn có thể dùng các tên nhóm cho nhanh như `group:fs` (mọi công cụ về file) hay `group:runtime` (mọi công cụ chạy lệnh shell).

## Lỗi "Nhà tù Sandbox" (Sandbox jail)
Đây là tình trạng Agent có công cụ nhưng không thể làm được gì hữu ích vì nó bị nhốt quá kỹ.
- **Triệu chứng**: Agent báo lỗi "Blocked by sandbox tool policy".
- **Cách sửa**: Nới lỏng cấu hình trong mục `tools.sandbox.tools.allow` hoặc chuyển chế độ sang `mode: "off"` nếu bạn đang dùng một mình.

---
Tài liệu liên quan: [Cơ chế cô lập (Sandboxing)](./sandboxing.vi.md), [Chế độ ưu tiên](../../tools/elevated.vi.md).
