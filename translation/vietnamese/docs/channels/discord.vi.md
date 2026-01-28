---
summary: "Trạng thái hỗ trợ, khả năng và cấu hình cho bot Discord"
read_when:
  - Bạn đang thiết lập hoặc tùy chỉnh kênh Discord
---
# Discord (Bot API)

Trạng thái: Sẵn sàng cho tin nhắn trực tiếp (DM) và các kênh văn bản trong máy chủ (guild) thông qua hệ thống bot chính thức của Discord.

## Thiết lập nhanh (cho người mới)
1) Tạo một Discord bot trên trang web Developer Portal và sao chép **Bot Token**.
2) Trong phần cài đặt bot, hãy bật **Message Content Intent** (và **Server Members Intent** nếu bạn muốn dùng danh sách trắng theo tên).
3) Cấu hình Token cho Moltbot:
   - Dùng biến môi trường: `DISCORD_BOT_TOKEN=...`
   - Hoặc tệp cấu hình: `channels.discord.token: "..."`.
4) Mời bot vào máy chủ của bạn với các quyền nhắn tin và đọc lịch sử.
5) Chạy Gateway. Lần đầu nhắn tin trực tiếp với bot, nó sẽ gửi một mã ghép nối (pairing code), hãy phê duyệt bằng lệnh `moltbot pairing approve discord <code>`.

## Cách thức hoạt động
- **Tin nhắn trực tiếp (DM)**: Sẽ được gộp vào phiên làm việc chính (`main`) của agent.
- **Kênh máy chủ**: Mỗi kênh sẽ có một phiên làm việc riêng biệt.
- **Quyền hạn**: Bot yêu cầu các quyền "Privileged Gateway Intents" (đặc biệt là nội dung tin nhắn) để có thể đọc được yêu cầu của bạn.
- **Lệnh gạch chéo (Slash commands)**: Moltbot hỗ trợ các lệnh gốc của Discord (như `/help`, `/status`).

## Cấu hình mẫu
```json5
{
  channels: {
    discord: {
      enabled: true,
      token: "YOUR_BOT_TOKEN",
      guilds: {
        "YOUR_GUILD_ID": {
          requireMention: true, // Chỉ trả lời khi được nhắc tên (@bot)
          channels: {
            "help": { allow: true }
          }
        }
      }
    }
  }
}
```

## Lưu ý về bảo mật
- Hãy giữ Bot Token cẩn thận như mật khẩu của bạn.
- Mặc định, bot sẽ yêu cầu ghép nối (pairing) cho các tin nhắn DM để đảm bảo chỉ những người được phép mới có thể sử dụng.
- Bạn có thể giới hạn bot chỉ hoạt động trong một số máy chủ hoặc kênh cụ thể bằng danh sách trắng (allowlist).

---
Tài liệu liên quan: [Lệnh gạch chéo](../tools/slash-commands.vi.md), [Ghép nối thiết bị](../../start/pairing.vi.md).
