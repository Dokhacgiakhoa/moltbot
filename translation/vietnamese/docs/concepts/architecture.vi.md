---
summary: "Kiến trúc Gateway WebSocket, các thành phần và luồng hoạt động của ứng dụng khách (client)"
read_when:
  - Bạn đang làm việc với giao thức Gateway, các ứng dụng khách hoặc phương thức truyền tải dữ liệu
---

# Kiến trúc Gateway

Cập nhật lần cuối: 22/01/2026

## Tổng quan

- Một tiến trình **Gateway** duy nhất chạy nền, quản lý tất cả các bề mặt nhắn tin (WhatsApp qua Baileys, Telegram qua grammY, Slack, Discord, Signal, iMessage, WebChat).
- Các ứng dụng khách điều khiển (ứng dụng macOS, CLI, giao diện web, hệ thống tự động hóa) kết nối tới Gateway thông qua **WebSocket** trên địa chỉ host đã cấu hình (mặc định là `127.0.0.1:18789`).
- Các **Node** (trên máy macOS/iOS/Android/không giao diện) cũng kết nối qua **WebSocket**, nhưng khai báo vai trò là `role: node` với các khả năng và lệnh cụ thể.
- Chỉ có tối đa một Gateway trên mỗi máy chủ; đây là nơi duy nhất mở phiên làm việc WhatsApp.
- Một **máy chủ canvas** (mặc định cổng `18793`) cung cấp HTML có thể chỉnh sửa bởi Agent và giao diện A2UI.

## Thành phần và Luồng hoạt động

### Gateway (dịch vụ chạy ngầm - daemon)
- Duy trì kết nối với các nhà cung cấp chat (providers).
- Cung cấp API WebSocket có kiểu dữ liệu rõ ràng (yêu cầu, phản hồi, sự kiện đẩy từ máy chủ).
- Kiểm tra tính hợp lệ của các khung dữ liệu (frames) đến dựa trên JSON Schema.
- Phát ra các sự kiện như: `agent`, `chat`, `presence`, `health`, `heartbeat`, `cron`.

### Ứng dụng khách (Client - Ứng dụng Mac / CLI / Web quản trị)
- Mỗi ứng dụng khách sử dụng một kết nối WebSocket duy nhất.
- Gửi các gói yêu cầu (`health`, `status`, `send`, `agent`, `system-presence`).
- Đăng ký nhận các sự kiện (`tick`, `agent`, `presence`, `shutdown`).

### Các Node (Node - macOS / iOS / Android / Headless)
- Kết nối tới **cùng một máy chủ WebSocket** với vai trò `role: node`.
- Cung cấp định danh thiết bị khi kết nối; việc ghép nối dựa trên **thiết bị** (vai trò `node`) và được phê duyệt trong kho lưu trữ ghép nối thiết bị.
- Cung cấp các lệnh như `canvas.*`, `camera.*`, `screen.record`, `location.get`.

Chi tiết giao thức:
- [Giao thức Gateway](../gateway/protocol.vi.md)

### WebChat
- Giao diện người dùng tĩnh, sử dụng API WebSocket của Gateway để xem lịch sử chat và gửi tin nhắn.
- Trong các thiết lập từ xa, WebChat kết nối thông qua cùng một đường truyền tunnel SSH hoặc Tailscale như các ứng dụng khách khác.

## Vòng đời kết nối (Dành cho một client đơn lẻ)

```
Ứng dụng khách (Client)           Gateway
   |                                |
   |---- yêu cầu:connect ---------->|
   |<------ phản hồi (ok) ----------|   (hoặc phản hồi lỗi + đóng kết nối)
   |   (dữ liệu hello-ok kèm ảnh chụp trạng thái: hiện diện + sức khỏe)
   |                                |
   |<------ sự kiện:presence -------|
   |<------ sự kiện:tick -----------|
   |                                |
   |------- yêu cầu:agent ---------->|
   |<------ phản hồi:agent ---------|   (Xác nhận: {runId, status: "accepted"})
   |<------ sự kiện:agent ----------|   (Đang truyền tin - streaming)
   |<------ phản hồi:agent ---------|   (Kết thúc: {runId, status, summary})
   |                                |
```

## Giao thức truyền tin (Tóm tắt)

- Phương thức truyền tải: WebSocket, các khung văn bản với dữ liệu JSON.
- Khung dữ liệu đầu tiên **phải** là `connect`.
- Sau bước bắt tay (handshake):
  - Yêu cầu (Requests): `{type:"req", id, method, params}` → `{type:"res", id, ok, payload|error}`
  - Sự kiện (Events): `{type:"event", event, payload, seq?, stateVersion?}`
- Nếu `CLAWDBOT_GATEWAY_TOKEN` (hoặc cờ `--token`) được thiết lập, tham số `connect.params.auth.token` phải khớp, nếu không kết nối sẽ bị đóng.
- Khóa phi biến (Idempotency keys) là bắt buộc đối với các phương thức có tác động thay đổi dữ liệu (`send`, `agent`) để có thể thử lại an toàn; máy chủ sẽ giữ một bộ nhớ đệm ngắn hạn để chống trùng lặp.

## Ghép nối & Tin cậy cục bộ

- Tất cả các khách WebSocket (người vận hành + các node) đều phải gửi **định danh thiết bị** khi `connect`.
- Các ID thiết bị mới yêu cầu phê duyệt ghép nối; Gateway sẽ cấp một **token thiết bị** cho các lần kết nối sau.
- Các kết nối **cục bộ** (truy cập qua loopback hoặc địa chỉ Tailscale của chính máy chủ đó) có thể được tự động phê duyệt để trải nghiệm người dùng trên cùng một máy được mượt mà.
- Các kết nối **không cục bộ** phải ký xác nhận `connect.challenge` và yêu cầu phê duyệt thủ công rõ ràng.
- Xác thực Gateway (`gateway.auth.*`) vẫn áp dụng cho **tất cả** các kết nối, dù là tại chỗ hay từ xa.

Chi tiết: [Giao thức Gateway](../gateway/protocol.vi.md), [Ghép nối](../start/pairing.vi.md), [Bảo mật](../gateway/security/index.vi.md).

## Truy cập từ xa

- Cách khuyên dùng: Tailscale hoặc VPN.
- Cách thay thế: Tunnel SSH
  ```bash
  ssh -N -L 18789:127.0.0.1:18789 user@host
  ```
- Các bước bắt tay và mã token xác thực vẫn áp dụng tương tự qua đường truyền tunnel.

---
Tài liệu liên quan: [Cấu hình Gateway](../gateway/configuration.vi.md), [Xử lý lỗi](../gateway/troubleshooting.vi.md).
