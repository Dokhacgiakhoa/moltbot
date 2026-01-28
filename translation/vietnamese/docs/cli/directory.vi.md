---
summary: "Tài liệu tham khảo lệnh `moltbot directory` (Tra cứu cá nhân, bạn bè, nhóm)"
read_when:
  - Bạn muốn tìm ID của một người dùng hoặc nhóm chat để gửi tin nhắn qua CLI
---

# `moltbot directory`

Tra cứu danh bạ cho các kênh có hỗ trợ (bao gồm liên hệ cá nhân, nhóm và thông tin của chính bot).

## Ví dụ sử dụng

```bash
# Liệt kê danh sách người dùng trên Slack có chứa chữ "U0"
moltbot directory peers list --channel slack --query "U0"

# Lấy ID của chính mình trên Zalo
moltbot directory self --channel zalouser

# Liệt kê thông tin thành viên trong một nhóm cụ thể
moltbot directory groups members --channel zalouser --group-id <id_nhom>
```

## Mục đích sử dụng
Lệnh `directory` được thiết kế để giúp bạn lấy các ID chính xác mà bạn có thể sao chép và dán vào các lệnh khác, đặc biệt là lệnh gửi tin nhắn:
```bash
moltbot message send --channel slack --target user:U012ABCDEF --message "Chào bạn!"
```

## Định dạng ID theo từng kênh:
- **WhatsApp**: Số điện thoại `+84...` hoặc mã JID nhóm.
- **Telegram**: `@tên_người_dùng` hoặc ID số.
- **Slack/Discord**: Định dạng `user:<id>` hoặc `channel:<id>`.
- **Zalo**: ID người dùng hoặc ID cuộc trò chuyện.

---
Tài liệu liên quan: [Gửi tin nhắn](./message.vi.md), [Cấu hình kênh](../channels/index.vi.md).
