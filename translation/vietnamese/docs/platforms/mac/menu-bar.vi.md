---
summary: "Logic trạng thái của thanh menu và các thông tin hiển thị cho người dùng"
read_when:
  - Bạn muốn điều chỉnh giao diện hoặc logic hiển thị trạng thái trên máy Mac
---

# Logic Trạng thái trên Thanh Menu

## Những gì được hiển thị
- Ứng dụng hiển thị trạng thái làm việc của Agent thông qua biểu tượng và dòng trạng thái đầu tiên trong menu xổ xuống.
- Thông tin về "Sức khỏe" (Health) sẽ bị ẩn đi khi Agent đang bận và tự động hiện lại khi Agent rảnh.
- Mục **"Nodes"** trong menu liệt kê các thiết bị đã ghép nối thành công.

## Các loại hoạt động (Activity kinds)
Khi Agent làm việc, bạn sẽ thấy các biểu tượng (glyph) tương ứng:
- `exec` (Chạy lệnh) → 💻
- `read` (Đọc tệp) → 📄
- `write` (Ghi tệp) → ✍️
- `edit` (Chỉnh sửa) → 📝
- `attach` (Gắn kèm) → 📎
- Mặc định → 🛠️

## Logic hiển thị văn bản
- **Khi làm việc**: Hiển thị theo dạng `<Vai trò phiên> · <nhãn hoạt động>`.
  - Ví dụ: `Main · exec: pnpm test` (Phiên chính đang chạy lệnh kiểm thử).
- **Khi rảnh**: Quay về hiển thị tóm tắt tình trạng kết nối (Health summary).

---
Tài liệu liên quan: [Trạng thái biểu tượng](./icon.vi.md), [Đánh giá sức khỏe](./health.vi.md).
