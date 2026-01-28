---
summary: "Thiết lập bot Mattermost và cấu hình cho Moltbot"
read_when:
  - Bạn đang sử dụng Mattermost cho đội ngũ và muốn tích hợp AI
---
# Mattermost (Plugin)

Moltbot hỗ trợ tích hợp với **Mattermost** - một nền tảng nhắn tin dành cho doanh nghiệp có thể tự lưu trữ (self-host).

## Cài đặt Plugin
Plugin Mattermost không được đi kèm sẵn khi cài đặt gốc, bạn cần cài đặt nó qua lệnh:
```bash
moltbot plugins install @moltbot/mattermost
```

## Thiết lập nhanh
1. **Tạo Bot**: Truy cập vào Mattermost, tạo một tài khoản Bot mới và sao chép mã **Bot Token**.
2. **Địa chỉ máy chủ**: Lấy URL máy chủ Mattermost của bạn (Ví dụ: `https://chat.congty.com`).
3. **Cấu hình Moltbot.json**:
   ```json5
   {
     channels: {
       mattermost: {
         enabled: true,
         botToken: "mm-token-cua-ban",
         baseUrl: "https://chat.congty.com",
         dmPolicy: "pairing"
       }
     }
   }
   ```

## Các chế độ trò chuyện (`chatmode`)
Bạn có thể điều chỉnh cách bot phản hồi trong các kênh:
- `oncall` (Mặc định): Chỉ phản hồi khi được `@nhắc_tên`.
- `onmessage`: Phản hồi mọi tin nhắn trong kênh.
- `onchar`: Chỉ phản hồi khi tin nhắn bắt đầu bằng một ký tự đặc biệt (ví dụ: `>` hoặc `!`).

## Kiểm soát quyền truy cập
- **Tin nhắn trực tiếp (DM)**: Mặc định sử dụng `pairing`. Bạn cần phê duyệt mã ghép đôi qua terminal để bắt đầu trò chuyện.
- **Kênh chat (Channels)**: Bạn có thể quy định danh sách người dùng (`groupAllowFrom`) hoặc các kênh thảo luận cụ thể được phép gọi bot.

## Giải quyết sự cố
- **Bot không phản hồi trong kênh**: Kiểm tra xem bạn đã mời bot vào kênh đó chưa. Nếu đang ở chế độ `oncall`, hãy đảm bảo bạn đã nhắc đúng tên bot.
- **Lỗi xác thực**: Kiểm tra lại `botToken` và đảm bảo máy chủ Mattermost của bạn có thể kết nối được từ internet hoặc từ máy chủ chạy Moltbot.

---
Tài liệu liên quan: [Cấu hình Gateway](../gateway/configuration.vi.md), [Plugin](../plugin.vi.md).
