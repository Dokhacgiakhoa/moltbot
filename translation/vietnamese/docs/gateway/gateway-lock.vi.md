---
summary: "Cơ chế bảo vệ để đảm bảo chỉ có duy nhất một thực thể Gateway hoạt động trên một cổng"
read_when:
  - Bạn gặp lỗi 'EADDRINUSE' hoặc báo lỗi có một bản Gateway khác đang chạy
---

# Khóa hạ tầng Gateway (Gateway lock)

## Tại sao cần cơ chế này?
- Đảm bảo chỉ có **duy nhất một thực thể Gateway** được phép chạy trên cùng một cổng (mặc định là 18789) trên cùng một máy tính.
- Ngăn chặn việc dữ liệu bị ghi đè lẫn nhau nếu có hai bản Bot cùng hoạt động.
- Phát hiện và báo lỗi ngay lập tức nếu cổng giao tiếp đã bị chiếm dụng.

## Cơ chế hoạt động
Moltbot sử dụng chính cổng giao tiếp TCP (WebSocket) làm khóa bảo vệ:
- Khi khởi động, Gateway sẽ cố gắng chiếm dụng cổng 18789.
- Nếu cổng này đã được một chương trình khác sử dụng, hệ thống sẽ báo lỗi `GatewayLockError` và dừng lại ngay lập tức.
- Khi Gateway dừng lại (hoặc bị treo máy, bị tắt đột ngột), hệ điều hành sẽ tự động giải phóng cổng này. Không cần tệp tin khóa tạm thời nào, giúp tránh việc bị treo khóa khi máy tính bị sập nguồn.

## Cách xử lý khi gặp lỗi khóa
Nếu bạn thấy thông báo lỗi "another gateway instance is already listening":
1. Kiểm tra xem bạn có đang chạy Moltbot ở một cửa sổ Terminal khác hay không.
2. Nếu bạn dùng ứng dụng Mac, hãy kiểm tra thanh Menu xem Bot có đang chạy ngầm không.
3. Nếu bạn muốn chạy hai bản Bot cùng lúc, bạn phải cấu hình chúng sử dụng hai cổng khác nhau (ví dụ: 18789 và 18790).

---
Tài liệu liên quan: [Lệnh Doctor](./doctor.vi.md), [Cấu hình cổng Gateway](./configuration.vi.md).
