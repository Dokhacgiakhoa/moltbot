---
summary: "Hướng dẫn vận hành dịch vụ Gateway, vòng đời và các thao tác kỹ thuật"
read_when:
  - Bạn muốn tìm hiểu cách vận hành máy chủ Moltbot
---

# Hướng dẫn vận hành Gateway

Hạ tầng Gateway là tiến trình chạy liên tục (always-on), đóng vai trò làm cầu nối cho các kênh nhắn tin (WhatsApp, Telegram) và quản lý tất cả các kết nối từ ứng dụng khách.

## Cách khởi động
```bash
moltbot gateway
```
Để xem nhật ký chi tiết ngay trên màn hình:
```bash
moltbot gateway --verbose
```
Nếu cổng 18789 đang bị chiếm dụng, bạn có thể dùng lệnh `--force` để ngắt các tiến trình cũ và khởi động lại.

## Các đặc điểm chính
- **Cấu hình tự động nạp lại**: Khi bạn sửa tệp `moltbot.json`, Gateway sẽ tự động cập nhật các thay đổi mà thường không cần khởi động lại toàn bộ tiến trình.
- **Dịch vụ đa năng**: Một cổng duy nhất (18789) vừa dùng cho kết nối WebSocket của ứng dụng, vừa dùng cho các API HTTP và Control UI.
- **Tự động lưu nhật ký**: Mọi hoạt động được ghi vào thư mục `/tmp/moltbot/`.
- **Bảo mật**: Yêu cầu Token xác thực theo mặc định. Bạn có thể thiết lập mã này trong tệp cấu hình.

## Truy cập từ xa
Moltbot được thiết kế để kết nối an toàn. Bạn nên sử dụng **Tailscale** hoặc **VPN** để truy cập Gateway từ xa. Nếu không có các công cụ đó, bạn có thể sử dụng giải pháp chuyển tiếp cổng qua SSH:
```bash
ssh -L 18789:127.0.0.1:18789 user@dia-chi-may-chu
```

## Quản lý dịch vụ (CLI)
Sử dụng các lệnh sau để điều khiển Gateway một cách chuyên nghiệp:
- `moltbot gateway status`: Kiểm tra xem máy chủ có đang chạy không.
- `moltbot gateway install`: Cài đặt Gateway thành một dịch vụ hệ thống (tự động chạy khi mở máy).
- `moltbot gateway stop`: Dừng dịch vụ.
- `moltbot logs --follow`: Theo dõi nhật ký hệ thống trực tiếp.

## Mô hình Bot cứu hộ (Rescue-Bot)
Nếu bạn lo lắng về việc Bot gặp lỗi và không thể liên lạc được, bạn có thể chạy một bản Gateway thứ hai độc lập hoàn toàn (sử dụng cổng khác và thư mục dữ liệu khác) để làm phương án cứu hộ.

---
Tài liệu liên quan: [Cấu hình chi tiết](./configuration.vi.md), [Khám phá mạng nội bộ](./bonjour.vi.md), [Truy cập từ xa](./remote.vi.md).
