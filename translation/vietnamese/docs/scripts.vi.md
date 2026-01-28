---
summary: "Các kịch bản (scripts) trong kho lưu trữ: Mục đích, phạm vi và lưu ý an toàn"
---
# Kịch bản hỗ trợ (Scripts)

Thư mục `scripts/` chứa các kịch bản hỗ trợ cho quy trình làm việc cục bộ và các tác vụ vận hành hệ thống. Hãy sử dụng các kịch bản này khi công việc cụ thể được gắn liền với chúng; nếu không, hãy ưu tiên sử dụng giao diện dòng lệnh (CLI).

## Quy ước

- Các kịch bản là **tùy chọn** trừ khi được nhắc đến trong tài liệu hoặc danh mục kiểm tra bản phát hành.
- Ưu tiên sử dụng CLI nếu có tính năng tương đương (ví dụ: việc theo dõi xác thực nên dùng lệnh `moltbot models status --check`).
- Các kịch bản có thể phụ thuộc vào môi trường máy chủ; hãy đọc mã nguồn trước khi chạy trên một máy tính mới.

## Git hooks

- `scripts/setup-git-hooks.js`: Thiết lập `core.hooksPath` cho các kho lưu trữ git.
- `scripts/format-staged.js`: Tự động định dạng mã nguồn (format) cho các tệp trong thư mục `src/` và `test/` trước khi commit.

## Theo dõi xác thực

Các kịch bản liên quan đến theo dõi xác thực (Auth monitoring) được mô tả chi tiết tại đây:
[/automation/auth-monitoring](../automation/auth-monitoring.vi.md)

## Lưu ý khi thêm kịch bản mới

- Giữ cho kịch bản tập trung vào một tác vụ cụ thể và có chú thích rõ ràng.
- Thêm mô tả ngắn gọn vào tài liệu hướng dẫn liên quan.

---
Tài liệu liên quan: [Tự động hóa](../automation/index.vi.md), [Hướng dẫn CLI](../cli/index.vi.md).
