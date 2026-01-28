---
summary: "Hướng dẫn chi tiết cách thiết lập Moltbot làm trợ lý cá nhân kèm các lưu ý an toàn"
read_when:
  - Bạn mới bắt đầu cài đặt trợ lý AI cá nhân
---
# Xây dựng trợ lý cá nhân với Moltbot (Phong cách Clawd)

Moltbot là một cổng kết nối (Gateway) đa kênh hỗ trợ WhatsApp, Telegram, Discord, iMessage và nhiều nền tảng khác. Hướng dẫn này sẽ giúp bạn thiết lập một "trợ lý cá nhân" thực thụ: một số điện thoại WhatsApp riêng biệt hoạt động như một quản gia AI luôn túc trực 24/7.

## ⚠️ An toàn là trên hết

Khi bạn cấu hình trợ lý, bạn đang cho phép AI:
- Chạy các lệnh trên máy tính của bạn (tùy vào các công cụ bạn cấp quyền).
- Đọc và ghi các tệp tin trong thư mục làm việc.
- Gửi tin nhắn phản hồi qua các kênh liên lạc.

Hãy bắt đầu một cách cẩn trọng:
- **Luôn giới hạn người dùng**: Sử dụng `allowFrom` để chỉ số điện thoại của bạn mới có quyền ra lệnh cho bot.
- **Dùng số điện thoại riêng**: Đừng dùng chung số cá nhân của bạn để tránh việc mọi tin nhắn rác đều bị AI xử lý.
- **Kiểm soát tính chủ động**: Mặc định bot sẽ tự kiểm tra công việc sau mỗi 30 phút (heartbeat). Nếu chưa tin tưởng, bạn có thể tắt tính năng này.

## Các bước chuẩn bị
- Máy tính đã cài **Node.js 22+**.
- Một số điện thoại thứ hai (SIM phụ hoặc eSIM) dành riêng cho trợ lý.
- Cài đặt Moltbot qua lệnh:
  ```bash
  npm install -g moltbot@latest
  ```

## Mô hình hoạt động khuyên dùng
Bạn nên sử dụng hai thiết bị:
1. **Điện thoại của bạn**: Dùng số cá nhân để nhắn tin ra lệnh.
2. **Điện thoại trợ lý**: Chứa số WhatsApp của bot, được kết nối với máy tính chạy Moltbot qua mã QR.

## Khởi động nhanh trong 5 phút
1. **Đăng nhập WhatsApp**: Chạy lệnh `moltbot channels login` và quét mã QR hiển thị trên màn hình bằng điện thoại trợ lý.
2. **Chạy Gateway**: Chạy lệnh `moltbot gateway` để giữ cho hệ thống luôn hoạt động.
3. **Cấu hình bảo mật**: Mở file `moltbot.json` và thêm số điện thoại của bạn vào danh sách được phép:
   ```json5
   {
     channels: { whatsapp: { allowFrom: ["+8490xxxxxxx"] } }
   }
   ```
4. **Trò chuyện**: Thử gửi một tin nhắn từ điện thoại của bạn tới số trợ lý.

## Không gian làm việc của trợ lý (Agent Workspace)
Mọi hướng dẫn vận hành, "trí nhớ" và tính cách của trợ lý sẽ được lưu trong một thư mục (mặc định là `~/clawd`). 
Moltbot sẽ tự động tạo các file quan trọng như:
- `SOUL.md`: Định hình tâm hồn và tính cách của bot.
- `AGENTS.md`: Các chỉ dẫn vận hành chi tiết.
- `IDENTITY.md`: Thông tin nhận diện của bot.
- `USER.md`: Thông tin về bạn (chủ nhân) để bot phục vụ tốt hơn.

## Tính chủ động (Heartbeats)
Đây là tính năng độc đáo giúp trợ lý của bạn không chỉ phản hồi khi được hỏi mà còn có thể tự động kiểm tra xem có việc gì cần làm không (như nhắc lịch hẹn, kiểm tra email...). Bạn có thể điều chỉnh tần suất hoặc tắt nó đi nếu muốn tiết kiệm chi phí API.

---
Tài liệu liên quan: [Cơ chế Trí nhớ](../../concepts/memory.vi.md), [Cấu hình hệ thống](../gateway/configuration.vi.md).
