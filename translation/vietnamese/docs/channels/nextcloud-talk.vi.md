---
summary: "Trạng thái hỗ trợ Nextcloud Talk, các khả năng và hướng dẫn cấu hình"
read_when:
  - Bạn muốn tích hợp Moltbot vào hệ thống Nextcloud của mình
---
# Nextcloud Talk (Plugin)

Moltbot hỗ trợ kết nối với **Nextcloud Talk** thông qua cơ chế Webhook Bot. Bạn có thể sử dụng bot để trò chuyện trực tiếp, thảo luận trong phòng chat và sử dụng các biểu tượng biểu cảm.

## Cài đặt Plugin
Nextcloud Talk được cung cấp dưới dạng plugin riêng biệt:
```bash
moltbot plugins install @moltbot/nextcloud-talk
```

## Các bước thiết lập nhanh
1. **Cài đặt Bot trên Nextcloud**: Sử dụng lệnh `occ` trên máy chủ Nextcloud của bạn để đăng ký bot:
   ```bash
   ./occ talk:bot:install "Moltbot" "ma_bi_mat_cua_ban" "url_webhook_cua_gateway" --feature reaction
   ```
2. **Kích hoạt Bot**: Trong cài đặt của phòng chat mục tiêu trên Nextcloud, hãy bật bot vừa tạo.
3. **Cấu hình Moltbot.json**:
   ```json5
   {
     channels: {
       "nextcloud-talk": {
         enabled: true,
         baseUrl: "https://cloud.congty.com",
         botSecret: "ma_bi_mat_cua_ban",
         dmPolicy: "pairing"
       }
     }
   }
   ```

## Các lưu ý quan trọng
- **Tin nhắn cũ**: Bot không thể tự bắt đầu cuộc trò chuyện trực tiếp (DM). Người dùng phải là người nhắn tin cho bot trước.
- **Dữ liệu truyền thông**: Hiện tại bot chưa hỗ trợ tải tệp tin gốc trực tiếp, các tệp tin sẽ được gửi dưới dạng đường dẫn URL.
- **Xác thực Webhook**: Nếu Gateway của bạn chạy sau một proxy, hãy đảm bảo cấu hình `webhookPublicUrl` chính xác để Nextcloud có thể gửi dữ liệu về.

## Kiểm soát quyền truy cập
- **Ghép đôi (Pairing)**: Mặc định người dùng mới sẽ nhận được mã ghép đôi và cần được phê duyệt qua terminal.
- **Phòng chat (Rooms)**: Bạn có thể sử dụng danh sách trắng (`rooms`) để quy định chính xác bot được phép hoạt động ở những phòng chat nào.

---
Tài liệu liên quan: [Cấu hình hệ thống](../gateway/configuration.vi.md), [Plugin](../../plugin.vi.md).
