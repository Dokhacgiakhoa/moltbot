---
summary: "TypeBox schema là nguồn sự thật duy nhất cho giao thức gateway"
read_when:
  - Cập nhật các schema giao thức hoặc tạo mã nguồn tự động
---
# TypeBox: Nguồn sự thật duy nhất của giao thức

Moltbot sử dụng TypeBox, một thư viện schema ưu tiên TypeScript, để định nghĩa **Giao thức Gateway WebSocket** (bắt tay, yêu cầu/phản hồi, sự kiện máy chủ).

Các schema này là nguồn duy nhất điều phối:
1. **Xác thực lúc chạy (Runtime validation)**: Đảm bảo dữ liệu gửi/nhận đúng định dạng.
2. **Xuất JSON Schema**: Để dùng cho các công cụ khác.
3. **Tạo mã Swift (Swift codegen)**: Cho ứng dụng macOS.

## Mô hình khái niệm
Mỗi tin nhắn qua Gateway WebSocket thuộc một trong ba khung (frames):
- **Yêu cầu (Request)**: `{ type: "req", id, method, params }`
- **Phản hồi (Response)**: `{ type: "res", id, ok, payload | error }`
- **Sự kiện (Event)**: `{ type: "event", event, payload, ... }`

Tin nhắn đầu tiên **bắt buộc** phải là yêu cầu `connect`. Sau đó, các ứng dụng khách có thể gọi các phương thức (như `send`, `chat.history`) hoặc đăng ký nhận các sự kiện (như `presence`, `agent`).

## Vị trí các tệp Schema
- Nguồn chính: `src/gateway/protocol/schema.ts`.
- Schema JSON đã tạo: `dist/protocol.schema.json`.
- Các model Swift cho app macOS: `apps/macos/Sources/MoltbotProtocol/GatewayModels.swift`.

## Quy trình làm việc khi thay đổi Schema
1. Cập nhật các schema TypeBox trong mã nguồn TypeScript.
2. Chạy lệnh `pnpm protocol:check` để kiểm tra và cập nhật các file tự động.
3. Commit các schema và model Swift đã được tạo mới vào kho lưu trữ (git).

Việc sử dụng TypeBox giúp đảm bảo rằng ứng dụng macOS và máy chủ Gateway luôn "nói cùng một ngôn ngữ" mà không cần phải viết code thủ công lặp lại ở cả hai nơi.

---
Tài liệu liên quan: [Kiến trúc Gateway](./architecture.vi.md), [Giao thức Gateway](../gateway/protocol.vi.md).
