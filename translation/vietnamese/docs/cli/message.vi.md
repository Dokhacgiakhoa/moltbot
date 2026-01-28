---
summary: "Tài liệu tham khảo lệnh `moltbot message` (Gửi tin nhắn + Tác vụ trên kênh)"
read_when:
  - Bạn muốn gửi tin nhắn hoặc thực hiện các hành động (react, edit, delete) trên các kênh chat qua CLI
---

# `moltbot message`

Một lệnh duy nhất để gửi tin nhắn và thực hiện các hành động trên các kênh (Discord, Google Chat, Slack, Mattermost, Telegram, WhatsApp, Signal, iMessage, MS Teams).

## Cách sử dụng

```bash
moltbot message <lệnh-con> [flags]
```

### Cách chọn mục tiêu (`--target`)
- **WhatsApp**: Số điện thoại chuẩn E.164 hoặc JID của nhóm.
- **Telegram**: ID cuộc trò chuyện hoặc `@tên-người-dùng`.
- **Discord**: `channel:<id>` hoặc `user:<id>`.
- **Slack**: `channel:<id>` hoặc `user:<id>`.
- **Signal**: `+Số-điện-thoại`, `group:<id>`.
- **MS Teams**: ID cuộc hội thoại hoặc `user:<aad-object-id>`.

## Các hành động chính

### 1. Gửi tin nhắn (`send`)
```bash
moltbot message send --target "+8490xxxxxxx" --message "Chào chủ nhân!"
```
- Hỗ trợ: Gửi tệp tin (`--media`), Trả lời tin nhắn cụ thể (`--reply-to`), Gửi vào luồng (`--thread-id`).

### 2. Tạo bình chọn (`poll`)
```bash
moltbot message poll --channel discord \
  --target channel:123 \
  --poll-question "Trưa nay ăn gì?" \
  --poll-option "Phở" --poll-option "Bún chả"
```
- Hỗ trợ trên: WhatsApp, Discord, MS Teams.

### 3. Tương tác cảm xúc (`react`)
```bash
moltbot message react --channel slack --target C123 --message-id 456 --emoji "✅"
```
- Hỗ trợ trên: Discord, Google Chat, Slack, Telegram, WhatsApp, Signal.

### 4. Các hành động khác
- `edit`: Sửa tin nhắn (Discord, Slack).
- `delete`: Xóa tin nhắn (Discord, Slack, Telegram).
- `pin` / `unpin`: Ghim hoặc bỏ ghim tin nhắn.
- `search`: Tìm kiếm tin nhắn (Discord).

## Broadcast (Gửi hàng loạt)
Sử dụng lệnh `broadcast` để gửi một thông điệp tới nhiều mục tiêu cùng lúc:
```bash
moltbot message broadcast --channel all --targets "+số_1" --targets "@user2" --message "Thông báo khẩn!"
```

---
Tài liệu liên quan: [Các lệnh Slash](../../tools/slash-commands.vi.md), [Cấu hình kênh](../channels/index.vi.md).
