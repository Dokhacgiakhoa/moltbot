---
summary: "Trạng thái hỗ trợ Matrix, các khả năng và hướng dẫn cấu hình"
read_when:
  - Bạn muốn kết nối Moltbot với mạng lưới Matrix hoặc Beeper
---
# Matrix (Plugin)

Matrix là một giao thức truyền thông mã nguồn mở và phi tập trung. Moltbot kết nối dưới tư cách là một **người dùng Matrix** trên bất kỳ máy chủ (homeserver) nào. Bạn cần tạo một tài khoản Matrix dành riêng cho bot.

## Quy trình cài đặt
Matrix được cung cấp dưới dạng plugin riêng biệt. Bạn cần cài đặt nó bằng lệnh:
```bash
moltbot plugins install @moltbot/matrix
```

## Các bước thiết lập
1. **Tạo tài khoản**: Bạn có thể tự chạy máy chủ Matrix hoặc đăng ký tại các dịch vụ phổ biến như `matrix.org`.
2. **Lấy mã Access Token**: Bạn có thể sử dụng API đăng nhập của Matrix để lấy mã này cho bot. Moltbot cũng hỗ trợ đăng nhập trực tiếp bằng `userId` và `password` ngay trong file cấu hình.
3. **Cấu hình**:
   ```json5
   {
     channels: {
       matrix: {
         enabled: true,
         homeserver: "https://matrix.example.org",
         accessToken: "MÃ_ACCESS_TOKEN_CỦA_BẠN",
         dm: { policy: "pairing" }
       }
     }
   }
   ```

## Mã hóa đầu cuối (E2EE)
Moltbot hỗ trợ đầy đủ mã hóa đầu cuối thông qua bộ công cụ Rust SDK. 
- Để bật tính năng này, hãy đặt `channels.matrix.encryption: true`.
- Trong lần khởi động đầu tiên, bot sẽ yêu cầu "Xác minh thiết bị" (Device verification). Bạn cần mở ứng dụng Matrix của mình (như Element) để nhấn phê duyệt nhằm cho phép bot đọc được các tin nhắn đã mã hóa.

## Kiểm soát quyền truy cập
- **Tin nhắn trực tiếp (DM)**: Mặc định sử dụng cơ chế ghép đôi (`pairing`).
- **Phòng chat (Groups)**: Sử dụng danh sách trắng (`allowlist`). Bạn có thể chỉ định ID các phòng chat hoặc bí danh (alias) mà bot được phép tham gia. 
- **Nhắc tên (Mentions)**: Mặc định bot chỉ hồi âm khi được nhắc tên trong các phòng chat công cộng để tránh làm phiền người dùng.

## Các tính năng hỗ trợ
- ✅ Trò chuyện trực tiếp và Phòng chat.
- ✅ Phản hồi theo luồng (Threads).
- ✅ Truyền tải tệp tin và ảnh.
- ✅ Biểu tượng cảm xúc (Reactions).
- ✅ Vị trí địa lý.

---
Tài liệu liên quan: [Plugin Moltbot](../../plugin.vi.md), [Cơ chế Ghép đôi](../../start/pairing.vi.md).
