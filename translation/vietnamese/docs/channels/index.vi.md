---
summary: "Các nền tảng nhắn tin mà Moltbot có thể kết nối"
read_when:
  - Bạn muốn chọn một kênh chat cho Moltbot
  - Bạn cần xem tổng quan nhanh về các nền tảng được hỗ trợ
---
# Các kênh Chat (Chat Channels)

Moltbot có thể trò chuyện với bạn trên bất kỳ ứng dụng chat nào bạn đang dùng. Mỗi kênh kết nối thông qua Gateway.
Văn bản được hỗ trợ ở mọi nơi; hình ảnh/âm thanh và cảm xúc (reactions) thay đổi tùy theo từng kênh.

## Các kênh được hỗ trợ

- [WhatsApp](./whatsapp.vi.md) — Phổ biến nhất; sử dụng thư viện Baileys và yêu cầu quét mã QR.
- [Telegram](./telegram.vi.md) — Sử dụng Bot API qua grammY; hỗ trợ rất tốt cho các nhóm (groups).
- [Discord](./discord.vi.md) — Discord Bot API; hỗ trợ server, channel và DM.
- [Slack](./slack.vi.md) — Sử dụng Bolt SDK; ứng dụng cho không gian làm việc.
- [Google Chat](./googlechat.vi.md) — Google Chat API thông qua HTTP webhook.
- [Signal](./signal.vi.md) — Sử dụng `signal-cli`; tập trung vào quyền riêng tư.
- [Zalo](./zalo.vi.md) — Zalo Bot API; ứng dụng nhắn tin phổ biến tại Việt Nam (plugin cài riêng).
- [Zalo Cá nhân (Zalo Personal)](./zalouser.vi.md) — Tài khoản Zalo cá nhân qua đăng nhập mã QR (plugin cài riêng).
- [iMessage](./imessage.vi.md) — Chỉ dành cho macOS; tích hợp gốc qua imsg (khuyên dùng BlueBubbles cho các thiết lập mới).
- [WebChat](../web/webchat.vi.md) — Giao diện WebChat của Gateway qua WebSocket.

## Ghi chú

- Các kênh có thể chạy đồng thời; bạn có thể cấu hình nhiều kênh và Moltbot sẽ điều hướng theo từng chat.
- Thiết lập nhanh nhất thường là **Telegram** (chỉ cần mã token của bot). WhatsApp yêu cầu ghép đôi qua QR và lưu trữ nhiều trạng thái hơn trên đĩa.
- Hành vi trong nhóm chat khác nhau tùy theo từng kênh; xem [Nhóm chat](../concepts/groups.vi.md).
- Việc ghép nối DM (DM pairing) và danh sách phê duyệt (allowlists) được thực thi để đảm bảo an toàn; xem [Bảo mật](../gateway/security.vi.md).
- Tài liệu hướng dẫn sửa lỗi: [Khắc phục lỗi kênh](./troubleshooting.vi.md).
