---
summary: "Cơ chế ghép nối thiết bị do Gateway quản lý dành cho iOS và các thiết bị từ xa"
read_when:
  - Bạn muốn cấp quyền cho một điện thoại hoặc máy tính khác truy cập vào Moltbot
---

# Cơ chế ghép nối do Gateway quản lý

Moltbot sử dụng Gateway làm "nguồn sự thật duy nhất" để quyết định những thiết bị nào được phép kết nối. Các ứng dụng khác (như ứng dụng Mac) chỉ đóng vai trò là giao diện hiển thị để bạn bấm nút Duyệt hoặc Từ chối các yêu cầu đang chờ.

## Các khái niệm cơ bản
- **Yêu cầu đang chờ (Pending)**: Một thiết bị vừa yêu cầu tham gia mạng lưới, cần bạn cho phép.
- **Thiết bị đã ghép nối (Paired)**: Đã được duyệt và được cấp một Token xác thực riêng.
- **Thời hạn chờ**: Các yêu cầu thường hết hạn sau **5 phút** nếu không được xử lý.

## Quy trình thực hiện qua dòng lệnh (CLI)
Nếu bạn không dùng giao diện ứng dụng Mac, bạn có thể thực hiện mọi thứ qua Terminal:
- `moltbot nodes pending`: Liệt kê các yêu cầu đang chờ.
- `moltbot nodes approve <ID>`: Phê duyệt một thiết bị.
- `moltbot nodes status`: Xem danh sách các thiết bị đang kết nối và quyền hạn của chúng.

## Tự động phê duyệt
Nếu bạn đang kết nối từ cùng một máy tính đang chạy Gateway (localhost) hoặc qua một đường truyền SSH mà Moltbot có thể xác thực, hệ thống có thể sẽ tự động phê duyệt thiết bị đó để giúp bạn tiết kiệm thời gian.

## Lưu ý về bảo mật
Mỗi thiết bị khi được duyệt sẽ nhận được một Token bí mật. Hãy coi Token này như mật khẩu của bạn. Nếu bạn đổi thiết bị hoặc muốn thu hồi quyền truy cập, hãy xóa thiết bị đó khỏi danh sách trong tệp cấu hình hoặc dùng lệnh `moltbot nodes reject`.

---
Tài liệu liên quan: [Quản lý thiết bị qua CLI](../cli/devices.vi.md), [Giao thức Gateway](./protocol.vi.md).
