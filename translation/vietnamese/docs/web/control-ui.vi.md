---
summary: "Giao diện điều khiển trên trình duyệt cho Gateway (chat, quản lý nút mạng, cấu hình)"
read_when:
  - Bạn muốn điều khiển Moltbot từ trình duyệt mà không cần dùng Terminal
---

# Giao diện điều khiển (Control UI)

Control UI là một ứng dụng web nhỏ gọn được tích hợp sẵn vào Gateway, cho phép bạn quản lý mọi thứ qua trình duyệt:

- Địa chỉ mặc định: `http://<ip-cua-ban>:18789/`

## Cách mở nhanh (Tại máy cục bộ)

Nếu Gateway đang chạy trên máy tính của bạn, hãy mở:
- http://localhost:18789/

Nếu trang không tải được, hãy đảm bảo bạn đã khởi động Gateway bằng lệnh: `moltbot gateway`.

## Các tính năng chính (Hiện tại)
- **Trò chuyện (Chat)**: Chat trực tiếp với AI thông qua trình duyệt.
- **Quản lý kênh (Channels)**: Kiểm tra trạng thái WhatsApp/Telegram, quét mã QR để đăng nhập.
- **Tiến trình (Instances)**: Xem danh sách các thiết bị đang kết nối.
- **Phiên làm việc (Sessions)**: Quản lý các cuộc hội thoại, ghi đè cài đặt cho từng phiên riêng biệt.
- **Tác vụ định kỳ (Cron jobs)**: Thêm, sửa, xóa hoặc chạy các tác vụ tự động.
- **Kỹ năng (Skills)**: Cài đặt và cập nhật các kỹ năng mới cho Bot.
- **Nút mạng (Nodes)**: Quản lý các thiết bị ngoại vi như điện thoại iOS/Android.
- **Cấu hình (Config)**: Chỉnh sửa tệp cài đặt `moltbot.json` ngay trên giao diện web.
- **Nhật ký (Logs)**: Xem trực tiếp các dòng log hệ thống để gỡ lỗi.

## Truy cập từ xa an toàn (Khuyên dùng)

### Sử dụng Tailscale (Cách tốt nhất)
Thay vì mở cổng mạng nguy hiểm, hãy sử dụng Tailscale để truy cập an toàn từ bất cứ đâu:
```bash
moltbot gateway --tailscale serve
```
Sau đó bạn có thể truy cập qua địa chỉ: `https://<ten-thiet-bi-tailscale>/`

### Sử dụng mã Token
Nếu truy cập không phải từ máy cục bộ (localhost), hệ thống sẽ yêu cầu mã Token để bảo mật. Bạn có thể lấy mã này bằng lệnh:
`moltbot dashboard`
Lệnh này sẽ tạo ra một đường dẫn kèm mã truy cập an toàn cho bạn.

---
Tài liệu liên quan: [Cấu hình Gateway](../../gateway/configuration.vi.md), [Hướng dẫn Tailscale](../../gateway/tailscale.vi.md).
