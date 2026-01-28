---
summary: "Sử dụng công cụ apply_patch để thực hiện các chỉnh sửa trên nhiều tệp cùng lúc"
read_when:
  - Bạn cần chỉnh sửa mã nguồn trên nhiều file một cách chính xác
---
# Công cụ apply_patch

Công cụ `apply_patch` cho phép bạn áp dụng các thay đổi tệp bằng định dạng bản vá (patch) có cấu trúc. Đây là cách lý tưởng để thực hiện các chỉnh sửa trên nhiều tệp hoặc nhiều đoạn mã khác nhau mà lệnh `edit` thông thường khó xử lý một cách ổn định.

## Cách sử dụng
Công cụ nhận một chuỗi `input` bao gồm một hoặc nhiều thao tác trên tệp, được bao bọc giữa hai nhãn `*** Begin Patch` và `*** End Patch`:

```
*** Begin Patch
*** Add File: đường/dẫn/đến/file.txt
+nội dung dòng 1
+nội dung dòng 2
*** Update File: src/main.ts
@@
-dòng cũ cần xóa
+dòng mới thay thế
*** Delete File: file_cu.txt
*** End Patch
```

## Các thông số
- `input` (bắt buộc): Nội dung đầy đủ của bản vá.

## Lưu ý
- Các đường dẫn tệp được tính tương đối từ thư mục gốc của không gian làm việc (workspace root).
- Bạn có thể đổi tên tệp bằng cách dùng `*** Move to:` bên trong phần `*** Update File:`.
- Tính năng này hiện đang ở chế độ **thử nghiệm** và mặc định bị tắt. Bạn có thể bật nó qua cấu hình `tools.exec.applyPatch.enabled`.
- Công cụ này hiện chỉ hỗ trợ các mô hình của OpenAI (bao gồm cả OpenAI Codex).

---
Tài liệu liên quan: [Cấu hình Kỹ năng](./skills-config.vi.md), [Thực thi lệnh](./exec.vi.md).
