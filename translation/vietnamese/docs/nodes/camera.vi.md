---
summary: "Sử dụng Camera (iOS, Android, macOS) cho Bot: chụp ảnh (jpg) và quay clip ngắn (mp4)"
read_when:
  - Bạn muốn Bot có khả năng "nhìn" thông qua camera của điện thoại hoặc máy tính
---

# Thu thập hình ảnh từ Camera

Moltbot hỗ trợ Bot sử dụng camera để thực hiện các công việc:

- **Nút iOS/Android**: Chụp ảnh hoặc quay video ngắn trực tiếp từ ứng dụng Moltbot trên điện thoại.
- **Ứng dụng macOS**: Chụp ảnh hoặc quay video từ webcam của máy Mac.

Mọi quyền truy cập camera đều được **người dùng kiểm soát** thông qua cài đặt.

## Trên điện thoại (iOS/Android)

### Cài đặt người dùng
- Trong tab Settings → **Camera** → **Allow Camera**.
- Nếu tắt, các lệnh chụp ảnh sẽ trả về lỗi `CAMERA_DISABLED`.

### Các lệnh hỗ trợ
- `camera.list`: Liệt kê các camera khả dụng (trước, sau).
- `camera.snap`: Chụp một tấm ảnh. Bạn có thể chỉ định camera trước hoặc sau, độ phân giải và chất lượng ảnh.
- `camera.clip`: Quay một đoạn video ngắn (mặc định 3 giây, tối đa 60 giây, có thể kèm âm thanh).

### Yêu cầu ứng dụng đang mở (Foreground)
Để đảm bảo quyền riêng tư, các lệnh camera chỉ hoạt động khi ứng dụng Moltbot đang được mở trên màn hình điện thoại. Nếu ứng dụng đang chạy ngầm, lệnh sẽ thất bại.

## Trên máy tính macOS

### Cài đặt người dùng
Tính năng này mặc định bị **Tắt** để bảo vệ quyền riêng tư.
- **Settings → General → Allow Camera**.

### Sử dụng qua dòng lệnh (CLI)
Bạn có thể ra lệnh cho Bot chụp ảnh từ webcam máy Mac bằng lệnh:
```bash
moltbot nodes camera snap --node <id>
```
Lệnh này sẽ lưu ảnh vào một tệp tạm và hiển thị đường dẫn `MEDIA:<đường-dẫn>`.

## An toàn và giới hạn thực tế
- Các tệp ảnh được tự động nén để đảm bảo dung lượng dưới 5MB.
- Video clip được giới hạn dưới 60 giây để tránh việc truyền tải dữ liệu quá nặng gây treo hệ thống.
- Khi truy cập camera, hệ điều hành sẽ hiển thị thông báo/đèn tín hiệu để người dùng luôn biết khi nào camera đang hoạt động.

---
Tài liệu liên quan: [Cài đặt trên iOS](../platforms/ios.vi.md), [Cài đặt trên macOS](../platforms/macos.vi.md).
