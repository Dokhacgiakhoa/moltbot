---
summary: "Chế độ đặc quyền (Elevated Mode) và các lệnh chỉ dẫn `/elevated`"
read_when:
  - Bạn muốn điều chỉnh quyền hạn thực thi lệnh của AI
---
# Chế độ đặc quyền (`/elevated`)

## Chế độ đặc quyền làm gì?
- `/elevated on`: Chạy trên máy chủ Gateway và vẫn giữ cơ chế hỏi ý kiến người dùng trước khi thực thi lệnh (giống với `/elevated ask`).
- `/elevated full`: Chạy trên máy chủ Gateway và **tự động phê duyệt** mọi lệnh thực thi (bỏ qua bước xác nhận của người dùng).
- `/elevated off`: Tắt hoàn toàn chế độ đặc quyền. AI sẽ quay lại môi trường bị cô lập (sandbox) nếu có cấu hình.

## Đặc điểm quan trọng
- **Tính an toàn**: Lệnh này chỉ thay đổi hành vi khi AI đang chạy trong môi trường bị cô lập (sandboxed). Nếu không dùng sandbox, các lệnh thực thi mặc định đã chạy trên máy chủ thật.
- **Phạm vi tác động**: Bạn có thể gửi lệnh `/elevated` riêng lẻ để thiết lập cho toàn bộ phiên làm việc, hoặc đặt nó bên trong một tin nhắn để chỉ áp dụng cho riêng tin nhắn đó.
- **Xác thực người dùng**: Không phải ai cũng có thể dùng lệnh này. Moltbot kiểm tra "Danh sách trắng" (allowlist) để đảm bảo chỉ những người dùng tin cậy mới có thể nâng quyền cho AI.

## Thứ tự ưu tiên (Ưu tiên từ trên xuống)
1. Lệnh chỉ dẫn đi kèm trong tin nhắn (chỉ có tác dụng với tin nhắn đó).
2. Thiết lập cho phiên làm việc (đã gửi lệnh `/elevated` trước đó).
3. Thiết lập mặc định của hệ thống (trong file cấu hình).

## Cách kiểm tra trạng thái
Gửi tin nhắn chỉ chứa từ `/elevated` để xem AI hiện đang ở mức đặc quyền nào (off, ask, hay full).

## Phê duyệt và Danh sách trắng
- Bạn có thể giới hạn quyền nâng cấp đặc quyền này theo từng kênh (như Discord, WhatsApp) hoặc cho từng Agent cụ thể trong file cấu hình.
- Ví dụ, bạn có thể chỉ cho phép tài khoản WhatsApp của chính mình nâng quyền AI lên mức `full`, trong khi người dùng khác chỉ được ở mức `off`.

---
Tài liệu liên quan: [Phê duyệt thực thi lệnh](./exec-approvals.vi.md), [Môi trường cô lập (Sandbox)](../concepts/sandboxing.vi.md).
