---
summary: "iMessage qua máy chủ BlueBubbles trên macOS (REST gửi/nhận, trạng thái đang soạn, phản hồi, ghép đôi và các hành động nâng cao)."
read_when:
  - Thiết lập kênh iMessage thông qua BlueBubbles
---
# BlueBubbles (iMessage qua macOS REST)

Đây là một plugin giúp Moltbot giao tiếp với máy chủ BlueBubbles chạy trên macOS thông qua các giao thức HTTP. Đây là phương thức **được khuyên dùng cho iMessage** vì nó cung cấp bộ API phong phú và dễ thiết lập hơn so với phương thức truyền thống.

## Tổng quan
- Yêu cầu chạy trên macOS thông qua ứng dụng trợ giúp BlueBubbles ([bluebubbles.app](https://bluebubbles.app)).
- Khuyên dùng: macOS Sequoia (15). macOS Tahoe (26) cũng hoạt động, nhưng tính năng chỉnh sửa và cập nhật ảnh nhóm có thể gặp lỗi.
- Một số tính năng nổi bật: Chỉnh sửa tin nhắn, thu hồi, trả lời theo luồng (threading), hiệu ứng tin nhắn, quản lý nhóm.
- Hoạt động dựa trên Webhooks để nhận tin nhắn và REST API để gửi phản hồi.

## Thiết lập nhanh
1. Cài đặt máy chủ BlueBubbles trên máy Mac của bạn (theo hướng dẫn tại [bluebubbles.app/install](https://bluebubbles.app/install)).
2. Trong phần cấu hình của BlueBubbles, bật tính năng Web API và đặt mật khẩu.
3. Chạy lệnh `moltbot onboard` và chọn BlueBubbles, hoặc cấu hình thủ công trong `moltbot.json`:
   ```json5
   {
     channels: {
       bluebubbles: {
         enabled: true,
         serverUrl: "http://<IP_MÁY_MÁC>:1234",
         password: "mật_khẩu_của_bạn",
         webhookPath: "/bluebubbles-webhook"
       }
     }
   }
   ```
4. Chỉ định Webhook trong BlueBubbles tới Gateway của bạn (Ví dụ: `https://gateway-cua-ban:3000/bluebubbles-webhook?password=<mật_khẩu>`).

## Kiểm soát quyền truy cập
- **Tin nhắn trực tiếp (DM)**: Mặc định sử dụng cơ chế `pairing`. Người lạ nhắn tin sẽ nhận được mã ghép đôi và cần được bạn phê duyệt qua CLI (`moltbot pairing approve bluebubbles <MÃ>`).
- **Nhóm chat**: Có thể thiết lập chế độ `allowlist` để chỉ những người trong danh sách mới có thể ra lệnh cho bot.

## Các hành động nâng cao
BlueBubbles hỗ trợ rất nhiều hành động đặc thù của iMessage mà bạn có thể bật trong file cấu hình:
- **react**: Phản hồi bằng biểu tượng cảm xúc (tapback).
- **edit**: Chỉnh sửa nội dung tin nhắn đã gửi.
- **unsend**: Thu hồi tin nhắn.
- **sendWithEffect**: Gửi tin nhắn kèm hiệu ứng (như rầm rộ, nhẹ nhàng, phao hoa...).
- **sendAttachment**: Gửi tệp tin hoặc ghi âm giọng nói.

## Giải quyết sự cố
- Nếu bot không nhận được tin nhắn, hãy kiểm tra lại cấu hình Webhook và đảm bảo máy chủ BlueBubbles có thể truy cập được địa chỉ Gateway của bạn.
- Mã ghép đôi có hiệu lực trong **1 giờ**.
- Các tính năng chỉnh sửa/thu hồi yêu cầu macOS 13 trở lên.

---
Tài liệu liên quan: [Cơ chế Ghép đôi](../../start/pairing.vi.md), [Cấu hình hệ thống](../gateway/configuration.vi.md).
