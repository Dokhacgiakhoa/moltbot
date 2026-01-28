---
summary: "Tổng quan về ghép nối (Pairing): phê duyệt ai có thể nhắn tin trực tiếp (DM) cho bạn + những node nào có thể tham gia hệ thống"
read_when:
  - Thiết lập quyền kiểm soát truy cập DM
  - Ghép nối một node iOS/Android mới
  - Xem xét trạng thái bảo mật của Moltbot
---

# Ghép nối (Pairing)

“Ghép nối” (Pairing) là bước **phê duyệt của chủ sở hữu** một cách tường minh trong Moltbot.
Nó được sử dụng ở hai nơi:

1) **Ghép nối DM** (ai được phép trò chuyện với bot)
2) **Ghép nối Node** (những thiết bị/node nào được phép tham gia vào mạng lưới gateway)

Bối cảnh bảo mật: [Bảo mật](../gateway/security.vi.md)

## 1) Ghép nối DM (truy cập chat gửi đến)

Khi một kênh được cấu hình với chính sách DM là `pairing`, những người gửi không xác định sẽ nhận được một mã ngắn và tin nhắn của họ sẽ **không được xử lý** cho đến khi bạn phê duyệt.

Chính sách DM mặc định được tài liệu hóa tại: [Bảo mật](../gateway/security.vi.md)

Mã ghép nối:
- 8 ký tự, viết hoa, không chứa các ký tự dễ nhầm lẫn (`0O1I`).
- **Hết hạn sau 1 giờ**. Bot chỉ gửi tin nhắn ghép nối khi có một yêu cầu mới được tạo (khoảng một lần mỗi giờ cho mỗi người gửi).
- Các yêu cầu ghép nối DM đang chờ được giới hạn tối đa là **3 yêu cầu cho mỗi kênh** theo mặc định; các yêu cầu bổ sung sẽ bị bỏ qua cho đến khi có một yêu cầu hết hạn hoặc được phê duyệt.

### Phê duyệt người gửi

```bash
moltbot pairing list telegram
moltbot pairing approve telegram <MÃ_CODE>
```

Các kênh được hỗ trợ: `telegram`, `whatsapp`, `signal`, `imessage`, `discord`, `slack`.

### Nơi lưu trữ trạng thái

Được lưu trong thư mục `~/.clawdbot/credentials/`:
- Các yêu cầu đang chờ: `<kênh>-pairing.json`
- Danh sách phê duyệt (allowlist): `<kênh>-allowFrom.json`

Hãy coi những file này là thông tin nhạy cảm (chúng kiểm soát quyền truy cập vào trợ lý của bạn).


## 2) Ghép nối thiết bị Node (iOS/Android/macOS/headless nodes)

Các Node kết nối đến Gateway dưới dạng **thiết bị** với vai trò `role: node`. Gateway sẽ tạo ra một yêu cầu ghép nối thiết bị và cần phải được phê duyệt.

### Phê duyệt một thiết bị node

```bash
moltbot devices list
moltbot devices approve <requestId>
moltbot devices reject <requestId>
```

### Nơi lưu trữ trạng thái

Được lưu trong thư mục `~/.clawdbot/devices/`:
- `pending.json` (tồn tại ngắn hạn; tính bằng giây/phút trước khi hết hạn)
- `paired.json` (các thiết bị đã ghép nối + mã token)

### Ghi chú

- API cũ `node.pair.*` (CLI: `moltbot nodes pending/approve`) là một kho lưu trữ ghép nối riêng biệt do gateway quản lý. Các node WebSocket vẫn yêu cầu phải thực hiện ghép nối thiết bị.


## Tài liệu liên quan

- Mô hình bảo mật + prompt injection: [Bảo mật](../gateway/security.vi.md)
- Cập nhật an toàn (chạy doctor): [Cập nhật](../install/updating.vi.md)
- Cấu hình kênh:
  - Telegram: [Telegram](../channels/telegram.vi.md)
  - WhatsApp: [WhatsApp](../channels/whatsapp.vi.md)
  - Signal: [Signal](../channels/signal.vi.md)
  - iMessage: [iMessage](../channels/imessage.vi.md)
  - Discord: [Discord](../channels/discord.vi.md)
  - Slack: [Slack](../channels/slack.vi.md)
