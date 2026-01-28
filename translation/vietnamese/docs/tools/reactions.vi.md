---
summary: "Cơ chế biểu cảm (reactions) dùng chung cho tất cả các kênh"
read_when:
  - Bạn đang làm việc với các biểu cảm (thả tim/emoji) trên bất kỳ kênh chat nào
---
# Công cụ biểu cảm (Reactions)

Moltbot sử dụng một cơ chế biểu cảm thống nhất giữa các kênh chat:

- `emoji`: Bắt buộc phải cung cấp khi muốn thêm một biểu cảm.
- `emoji=""`: Xóa bỏ (các) biểu cảm của bot nếu kênh chat đó hỗ trợ.
- `remove: true`: Xóa một emoji cụ thể (yêu cầu phải cung cấp `emoji`).

## Lưu ý theo từng kênh:

- **Discord/Slack**: Để trống `emoji` sẽ xóa tất cả các biểu cảm của bot trên tin nhắn đó; `remove: true` sẽ chỉ xóa đúng emoji được chỉ định.
- **Google Chat**: Để trống `emoji` sẽ xóa biểu cảm của ứng dụng; `remove: true` xóa đúng emoji đó.
- **Telegram**: Để trống `emoji` sẽ xóa các biểu cảm của bot; `remove: true` cũng thực hiện việc xóa nhưng vẫn yêu cầu một chuỗi `emoji` không trống để vượt qua bước kiểm tra công cụ.
- **WhatsApp**: Để trống `emoji` sẽ xóa biểu cảm của bot.
- **Signal**: Các thông báo về biểu cảm gửi đến sẽ tạo ra các sự kiện hệ thống nếu tính năng `channels.signal.reactionNotifications` được bật.

---
Tài liệu liên quan: [Cấu hình các kênh](../channels/index.vi.md), [Ghép nối](../../start/pairing.vi.md).
