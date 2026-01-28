---
summary: "Giao thức Gateway WebSocket: Quy trình bắt tay, khung dữ liệu và phiên bản"
read_when:
  - Bạn đang lập trình một ứng dụng khách (Client) muốn giao tiếp trực tiếp với Moltbot
---

# Giao thức Gateway (WebSocket)

Giao thức Moltbot Gateway (WebSocket) là **trục xương sống kết nối** duy nhất cho mọi thành phần trong hệ thống. Tất cả các ứng dụng (CLI, giao diện web, ứng dụng Mac/iOS) đều kết nối qua WebSocket và khai báo **vai trò (role)** và **quyền hạn (scope)** của mình ngay từ bước đầu tiên.

## Quy trình Bắt tay (Handshake)
Mọi kết nối đều phải tuân thủ trình tự nghiêm ngặt:
1. **Gateway gửi thử thách (Challenge)**: Để đảm bảo kết nối hợp lệ.
2. **Client gửi yêu cầu kết nối**: Khai báo phiên bản, danh tính thiết bị và Token xác thực.
3. **Gateway xác nhận**: Nếu hợp lệ, Gateway trả về lời chào và các quy tắc hoạt động (như tần suất gửi tín hiệu giữ kết nối).

## Các cấu trúc dữ liệu chính (Framing)
Dữ liệu được trao đổi dưới dạng JSON với 3 loại khung hình:
- **Yêu cầu (req)**: Client hỏi hoặc ra lệnh.
- **Phản hồi (res)**: Gateway trả lời kết quả thành công hay thất bại.
- **Sự kiện (event)**: Gateway chủ động báo tin (ví dụ: có tin nhắn mới đến, Agent vừa trả lời xong).

## Vai trò trong hệ thống
- **Người điều hành (operator)**: Các ứng dụng dùng để điều khiển Bot (CLI, Giao diện quản lý).
- **Thiết bị hỗ trợ (node)**: Các thiết bị cung cấp kỹ năng cho Bot (ví dụ: điện thoại cung cấp Camera, máy tính cung cấp màn hình).

## Bảo mật và Xác thực
Gateway yêu cầu mỗi thiết bị phải có danh tính ổn định (`device.id`). 
- **Kết nối nội bộ**: Thường được ưu tiên hoặc tự động duyệt.
- **Kết nối từ bên ngoài**: Bắt buộc phải ký số vào bản tin "thử thách" để chứng minh danh tính.
- **Token thiết bị**: Sau khi ghép nối (pairing), thiết bị sẽ được cấp một Token riêng dùng cho những lần sau.

---
Tài liệu liên quan: [Cơ chế ghép nối](./pairing.vi.md), [Tổng quan về Gateway](./index.vi.md).
