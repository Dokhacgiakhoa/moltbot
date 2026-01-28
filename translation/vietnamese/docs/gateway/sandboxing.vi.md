---
summary: "Cơ chế cô lập của Moltbot: Các chế độ, không gian làm việc và Docker"
read_when:
  - Bạn muốn AI có quyền chạy lệnh shell nhưng lo ngại nó làm hỏng máy tính của bạn
---

# Cơ chế cô lập (Sandboxing)

Moltbot có thể chạy các **công cụ bên trong môi trường Docker** (Sandbox) để bảo vệ máy tính của bạn. Nếu bạn bật tính năng này, Agent vẫn hoạt động nhưng các lệnh nguy hiểm (như xóa file, cài đặt phần mềm) sẽ bị nhốt trong một "hộp cát" riêng biệt.

## Các chế độ Sandbox
Bạn có thể cấu hình chế độ này tại `agents.defaults.sandbox.mode`:
- **`off`**: Tắt cô lập hoàn toàn. Mọi thứ chạy trực tiếp trên máy của bạn (Hỗ trợ tốt nhất cho công việc cá nhân).
- **`non-main`**: Chỉ cô lập những người lạ nhắn tin đến hoặc những nhóm chat không phải do bạn quản lý.
- **`all`**: Cô lập mọi lúc, mọi nơi, cho mọi người.

## Quyền truy cập không gian làm việc
Bạn có thể chọn những gì Sandbox được phép nhìn thấy trên máy của bạn (`workspaceAccess`):
- **`none`**: Sandbox hoàn toàn bị ngắt kết nối với file của bạn. Nó có một thư mục riêng để làm việc.
- **`ro` (Chỉ đọc)**: Agent có thể đọc file của bạn nhưng không thể sửa hay xóa chúng.
- **`rw` (Đọc & Ghi)**: Agent có thể đọc và sửa file trong thư mục làm việc nhưng vẫn bị nhốt trong Docker (không thể truy cập các file hệ thống khác).

## Các bước thiết lập ban đầu
Để tính năng này hoạt động, bạn cần cài đặt Docker và chạy lệnh sau để chuẩn bị môi trường:
```bash
scripts/sandbox-setup.sh
```

## Những lưu ý quan trọng
- **Mạng máy tính**: Theo mặc định, Sandbox **không có internet**. Điều này để ngăn AI vô tình gửi dữ liệu của bạn ra ngoài. Bạn có thể bật lại internet trong cấu hình nếu cần.
- **Lệnh ưu tiên (Elevated)**: Có một số lệnh bạn có thể cấu hình để luôn chạy trực tiếp trên máy (không bị nhốt) nếu bạn hoàn toàn tin tưởng chúng.

---
Tài liệu liên quan: [So sánh Sandbox & Chính sách](./sandbox-vs-tool-policy-vs-elevated.vi.md), [Bảo mật](./security/index.vi.md).
