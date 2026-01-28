---
summary: "Thiết lập Slack cho chế độ Socket hoặc HTTP Webhook"
read_when:
  - Thiết lập Slack hoặc gỡ lỗi các chế độ Socket/HTTP
---
# Slack

## Chế độ Socket (Mặc định)

Đây là cách dễ nhất vì không yêu cầu địa chỉ HTTPS công khai.
1) Tạo một ứng dụng Slack trên [Slack API portal](https://api.slack.com/apps).
2) Bật **Socket Mode**. Tạo một **App Token** (bắt đầu bằng `xapp-`).
3) Trong mục **OAuth & Permissions**, cài đặt ứng dụng vào Workspace của bạn và lấy **Bot Token** (bắt đầu bằng `xoxb-`).
4) Bật **Event Subscriptions**, chọn các sự kiện quan trọng như `message.channels`, `app_mention`, và `reaction_added`.
5) Mời bot vào các kênh bạn muốn sử dụng.

## Chế độ HTTP (Events API)
Phù hợp khi Gateway của bạn có địa chỉ HTTPS công khai. Bạn sẽ cấu hình Slack gửi tin nhắn trực tiếp đến URL của bạn (mặc định là `/slack/events`).

## Luồng tin nhắn (Threading)
Moltbot hỗ trợ trả lời theo luồng (thread) để giữ cho kênh chat gọn gàng. Bạn có thể cấu hình:
- `off` (Mặc định): Chỉ trả lời trong luồng nếu tin nhắn gốc đã nằm trong một luồng.
- `first`: Tin nhắn đầu tiên sẽ tạo luồng mới, các tin nhắn sau đó (nếu có chia nhỏ) sẽ gửi vào kênh chính.
- `all`: Tất cả tin nhắn phản hồi đều nằm trong luồng.

## Bảo mật và Quyền hạn
- **Ghép nối (Pairing)**: Áp dụng cho tin nhắn trực tiếp để đảm bảo an toàn.
- **Danh sách trắng (Allowlist)**: Bạn có thể giới hạn bot chỉ hoạt động trong một số kênh hoặc cho một số người dùng cụ thể.
- **Mã thông báo người dùng (User Token)**: Moltbot có thể sử dụng thêm mã thông báo người dùng (`xoxp-`) để thực hiện các thao tác đọc lịch sử hoặc tìm kiếm mà bot thường không làm được.

## Cấu hình mẫu
```json5
{
  channels: {
    slack: {
      enabled: true,
      appToken: "xapp-...",
      botToken: "xoxb-...",
      groupPolicy: "allowlist",
      channels: {
        "#general": { "allow": true, "requireMention": true }
      }
    }
  }
}
```

---
Tài liệu liên quan: [Ghép nối thiết bị](../../start/pairing.vi.md), [Lệnh gạch chéo](../../tools/slash-commands.vi.md).
