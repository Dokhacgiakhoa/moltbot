---
summary: "Vòng đời của Gateway trên macOS (quản lý qua launchd)"
read_when:
  - Bạn muốn tìm hiểu cách ứng dụng Mac khởi động và quản lý tiến trình Gateway
---

# Vòng đời của Gateway trên macOS

Mặc định, ứng dụng macOS **quản lý Gateway thông qua dịch vụ launchd** và không khởi động Gateway như một tiến trình con trực tiếp của ứng dụng.

## Cơ chế hoạt động mặc định
1. Ứng dụng sẽ thử kết nối với một Gateway đang chạy sẵn trên cổng quy định.
2. Nếu không tìm thấy, nó sẽ kích hoạt dịch vụ `launchd` thông qua CLI `moltbot`.
3. Điều này giúp hệ thống có khả năng tự khởi động khi máy tính đăng nhập và tự động chạy lại nếu tiến trình bị sập.

## Chế độ Kết nối thuần túy (Attach-only)
Để ép buộc ứng dụng macOS **không bao giờ tự ý cài đặt hay quản lý launchd**, bạn có thể khởi chạy nó với tham số `--attach-only` (hoặc `--no-launchd`). Ở chế độ này, ứng dụng chỉ đóng vai trò là giao diện điều khiển cho một Gateway đã được bạn khởi chạy thủ công trước đó.

## Tại sao chúng tôi khuyên dùng launchd?
- **Tự động khởi động**: Bot luôn sẵn sàng ngay khi bạn mở máy.
- **Tiêu chuẩn hệ thống**: Tận dụng cơ chế giám sát tiến trình và ghi nhật ký (logs) chuyên nghiệp của macOS.

---
Tài liệu liên quan: [Cài đặt Gateway](../../gateway/index.vi.md), [Xử lý sự cố](../../gateway/troubleshooting.vi.md).
