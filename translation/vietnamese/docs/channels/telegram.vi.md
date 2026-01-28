---
summary: "Trạng thái hỗ trợ Telegram bot, các khả năng và cấu hình"
read_when:
  - Đang làm việc với các tính năng Telegram hoặc webhook
---
# Telegram (Bot API)

Trạng thái: Đã sẵn sàng cho thực tế (production-ready) cho tin nhắn trực tiếp (DM) và nhóm chat (groups) thông qua thư viện grammY. Sử dụng long-polling theo mặc định; webhook là tùy chọn.

## Thiết lập nhanh (Dành cho người mới)
1) Tạo một con bot với **@BotFather** trên Telegram và sao chép mã Token.
2) Thiết lập token trong cấu hình: `channels.telegram.botToken: "..."`.
3) Khởi động gateway.
4) Quyền truy cập DM mặc định là `pairing` (ghép đôi); hãy phê duyệt mã ghép đôi trong lần liên lạc đầu tiên.

Cấu hình tối thiểu:
```json5
{
  channels: {
    telegram: {
      enabled: true,
      botToken: "123:abc",
      dmPolicy: "pairing"
    }
  }
}
```

## Thiết lập Bot (Các bước nhanh)
### 1) Tạo bot token (BotFather)
- Mở Telegram và chat với **@BotFather**.
- Chạy lệnh `/newbot`, sau đó làm theo hướng dẫn (tên bot + username kết thúc bằng `bot`).
- Sao chép Token và lưu giữ an toàn.

Các thiết lập quan trọng trong BotFather:
- `/setjoingroups`: cho phép/chặn việc thêm bot vào nhóm.
- `/setprivacy`: kiểm soát việc bot có được xem mọi tin nhắn trong nhóm hay không. **Tắt (Disable)** nếu bạn muốn bot phản hồi mọi tin nhắn mà không cần @mention.

### 2) Quyền xem tin nhắn trong nhóm (Privacy Mode)
Mặc định các bot Telegram ở **Chế độ riêng tư (Privacy Mode)**, nghĩa là chúng chỉ thấy tin nhắn khi được @mention hoặc là lệnh (command).
Nếu bạn muốn bot thấy *tất cả* tin nhắn trong nhóm:
- Tắt chế độ riêng tư qua lệnh `/setprivacy` trong @BotFather.
- **Hoặc** thêm bot làm **Admin** của nhóm (bot admin luôn thấy mọi tin nhắn).

## Cách hoạt động
- Tin nhắn trong DM chia sẻ phiên làm việc chính của agent; tin nhắn trong nhóm được cô lập (`agent:<agentId>:telegram:group:<chatId>`).
- Phản hồi trong nhóm yêu cầu @mention bot theo mặc định.
- Bot Telegram không hỗ trợ thông báo đã đọc (read receipts).

## Lệnh (Commands)
Moltbot tự động đăng ký các lệnh hệ thống (như `/status`, `/reset`, `/model`) vào menu của bot Telegram khi khởi động.

Bạn có thể thêm các lệnh tùy chỉnh vào menu:
```json5
{
  channels: {
    telegram: {
      customCommands: [
        { command: "backup", description: "Sao lưu dữ liệu" },
        { command: "generate", description: "Tạo hình ảnh" }
      ]
    }
  }
}
```

## Chế độ kích hoạt trong nhóm
Mặc định bot chỉ trả lời khi được nhắc tên (@mention). Để thay đổi:

### Qua cấu hình:
```json5
{
  channels: {
    telegram: {
      groups: {
        "*": { requireMention: false }  // Trả lời mọi tin nhắn trong tất cả các nhóm
      }
    }
  }
}
```

### Qua lệnh chat (trong nhóm):
- `/activation always` - trả lời mọi tin nhắn.
- `/activation mention` - chỉ trả lời khi được nhắc tên.

## Các nút nhấn trực tiếp (Inline Buttons)
Telegram hỗ trợ bàn phím nội dòng với các nút phản hồi. Moltbot có thể gửi tin nhắn kèm các nút này và xử lý khi người dùng nhấn vào.

```json5
{
  "action": "send",
  "channel": "telegram",
  "to": "123456789",
  "message": "Hãy chọn một phương án:",
  "buttons": [
    [
      {"text": "Có", "callback_data": "yes"},
      {"text": "Không", "callback_data": "no"}
    ]
  ]
}
```

## Truyền phát dữ liệu (Streaming - Draft bubbles)
Telegram có thể hiển thị thanh "đang soạn tin" (draft bubbles) trong khi agent đang tạo câu trả lời. Điều này mang lại cảm giác mượt mà và bot đang thực sự suy nghĩ.

---
Tài liệu liên quan: [Cấu hình Gateway](../gateway/configuration.vi.md), [Ghép nối](../start/pairing.vi.md).
