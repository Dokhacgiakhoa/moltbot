---
summary: "Xác thực cấu hình nghiêm ngặt và quy trình di chuyển dữ liệu thông qua công cụ Doctor"
---

# Xác thực Cấu hình nghiêm ngặt (Doctor-only migrations)

## Mục tiêu
- **Từ chối các cài đặt không rõ nguồn gốc**: Bất kỳ từ khóa nào không nằm trong sơ đồ cấu hình chuẩn sẽ bị báo lỗi.
- **Bắt buộc có sơ đồ cho Plugin**: Các plugin không có tệp mô tả (manifest) và sơ đồ cài đặt (schema) sẽ không được tải.
- **Loại bỏ việc tự động sửa cài đặt**: Hệ thống sẽ không tự động chuyển đổi các cài đặt cũ khi khởi động; mọi thay đổi phải thông qua công cụ `doctor`.
- **Tự động kiểm tra khi khởi động**: Nếu cài đặt không hợp lệ, Bot sẽ không hoạt động cho đến khi lỗi được sửa.

## Tại sao cần làm vậy?
Việc kiểm soát chặt chẽ các cài đặt giúp hệ thống hoạt động ổn định hơn, tránh các lỗi tiềm ẩn do người dùng nhập sai tên biến hoặc sử dụng các biến cũ đã bị loại bỏ.

## Quy trình sử dụng công cụ Doctor
Mỗi khi bạn khởi động Bot, Moltbot sẽ tự động kiểm tra tệp cấu hình.
- Nếu tệp cấu hình có lỗi: Bot sẽ hiển thị danh sách các lỗi và yêu cầu bạn chạy lệnh: `moltbot doctor --fix`.
- Lệnh `moltbot doctor --fix` sẽ:
  - Tự động chuyển đổi các cài đặt cũ sang định dạng mới.
  - Loại bỏ các cài đặt rác hoặc viết sai chính tả.
  - Ghi lại tệp cấu hình đã được sửa đổi và cho phép Bot khởi động bình thường.

## Khi cấu hình bị lỗi, bạn có thể làm gì?
Bot sẽ tạm thời bị khóa hầu hết các tính năng trừ các lệnh chẩn đoán như:
- `moltbot doctor`: Kiểm tra và sửa lỗi.
- `moltbot logs`: Xem nhật ký lỗi.
- `moltbot status`: Kiểm tra trạng thái hệ thống.

---
Tài liệu liên quan: [Cấu hình Gateway](../../gateway/configuration.vi.md), [Xử lý sự cố](../../help/common-issues.vi.md).
