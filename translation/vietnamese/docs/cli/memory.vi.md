---
summary: "Tài liệu tham khảo lệnh `moltbot memory` (Trạng thái/Đánh chỉ mục/Tìm kiếm bộ nhớ)"
read_when:
  - Bạn muốn quản lý hoặc tìm kiếm thông tin trong bộ nhớ ngữ nghĩa (semantic memory) của Agent
---

# `moltbot memory`

Quản lý việc đánh chỉ mục và tìm kiếm bộ nhớ dữ liệu (semantic memory). Tính năng này được cung cấp bởi plugin bộ nhớ (mặc định là `memory-core`).

Tài liệu liên quan:
- Khái niệm bộ nhớ: [Trí nhớ Agent](../../concepts/memory.vi.md)

## Ví dụ sử dụng

```bash
# Xem trạng thái bộ nhớ hiện tại
moltbot memory status

# Kiểm tra sâu tình trạng vector và mô hình nhúng (embedding)
moltbot memory status --deep

# Thực hiện đánh lại chỉ mục toàn bộ dữ liệu (reindex)
moltbot memory index --verbose

# Tìm kiếm thông tin trong bộ nhớ
moltbot memory search "quy trình bàn giao dự án"
```

## Các tùy chọn
- `--agent <id>`: Chỉ thực hiện lệnh cho một Agent cụ thể (mặc định là tất cả).
- `--verbose`: Hiển thị chi tiết quá trình đánh chỉ mục (nguồn dữ liệu, mô hình đang dùng, các lô dữ liệu đang xử lý).

**Lưu ý**: Lệnh `memory status --deep --index` sẽ tự động thực hiện việc đánh chỉ mục lại nếu phát hiện dữ liệu hiện có đã bị cũ hoặc bị thay đổi.

---
Tài liệu liên quan: [Cấu hình Plugin](./plugins.vi.md).
