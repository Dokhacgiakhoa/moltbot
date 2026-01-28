---
summary: "Cấu hình và thiết lập bot chat cho Twitch"
read_when:
  - Bạn muốn tích hợp Moltbot vào luồng livestream trên Twitch
---
# Twitch (Plugin)

Moltbot hỗ trợ chat trên Twitch thông qua giao thức IRC. Bot sẽ tham gia vào luồng chat của bạn dưới tư cách là một người dùng Twitch bình thường để gửi và nhận tin nhắn.

## Cài đặt Plugin
Twitch được cung cấp dưới dạng plugin riêng biệt:
```bash
moltbot plugins install @moltbot/twitch
```

## Thiết lập nhanh (Dành cho người mới)
1. **Tạo tài khoản**: Bạn nên tạo một tài khoản Twitch riêng cho bot (để tránh nhầm lẫn với tài khoản cá nhân).
2. **Lấy mã Token**: Sử dụng công cụ [Twitch Token Generator](https://twitchtokengenerator.com/).
   - Chọn **Bot Token**.
   - Đảm bảo đã chọn quyền `chat:read` và `chat:write`.
   - Sao chép **Client ID** và **Access Token**.
3. **Cấu hình**:
   ```json5
   {
     channels: {
       twitch: {
         enabled: true,
         username: "ten_bot_cua_ban",
         accessToken: "oauth:abc123...", // Bắt đầu bằng oauth:
         clientId: "ma_client_id_cua_ban",
         channel: "ten_kenh_cua_ban",     // Tên kênh mà bot sẽ tham gia
         allowFrom: ["ID_nguoi_dung_cua_ban"] // Giới hạn người được điều khiển bot
       }
     }
   }
   ```

## Kiểm soát quyền truy cập
Trên Twitch chat, bất kỳ ai cũng có thể gõ phím. Vì vậy, việc thiết lập quyền là **cực kỳ quan trọng**:
- **Nhắc tên**: Mặc định bot chỉ phản hồi khi được `@nhắc_tên`.
- **Theo vai trò (`allowedRoles`)**: Bạn có thể quy định chỉ `moderator` (kiểm duyệt viên), `vip`, hoặc `subscriber` mới được dùng lệnh.
- **Theo ID người dùng (`allowFrom`)**: Cách an toàn nhất, chỉ những ID cụ thể mới có toàn quyền điều khiển bot.

## Tự động làm mới Token (Refresh Token)
Mã Token lấy từ trình tạo mã thường có thời hạn ngắn. Để bot chạy ổn định lâu dài, bạn nên đăng ký một ứng dụng trên [Twitch Developer Console](https://dev.twitch.tv/console) để lấy `clientSecret` và `refreshToken`. Khi đó, Moltbot sẽ tự động làm mới mã đăng nhập mỗi khi hết hạn.

## Các giới hạn
- Mỗi tin nhắn bị giới hạn ở **500 ký tự** (Hệ thống sẽ tự cắt nhỏ tin nhắn nếu dài hơn).
- Không hỗ trợ gửi các tệp tin đa phương tiện trực tiếp (hình ảnh, video) vào chat.

---
Tài liệu liên quan: [Cấu hình hệ thống](../gateway/configuration.vi.md), [Plugin](../../plugin.vi.md).
