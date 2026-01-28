---
summary: "Cách ứng dụng Mac nhúng giao diện WebChat của Gateway và phương pháp gỡ lỗi"
read_when:
  - Bạn muốn sử dụng giao diện chat trực tiếp trên thanh menu máy Mac
---

# Giao diện Chat (WebChat trên macOS)

Ứng dụng macOS nhúng giao diện WebChat của Gateway dưới dạng một cửa sổ SwiftUI bản địa. Nó kết nối tới Gateway và mặc định hiển thị **phiên chính (main session)** của Agent.

## Các chế độ kết nối
- **Cục bộ (Local)**: Kết nối trực tiếp tới Gateway chạy trên máy.
- **Từ xa (Remote)**: Tự động "bắc cầu" cổng điều khiển qua SSH để bạn có thể chat với Bot đang chạy trên máy chủ khác một cách mượt mà.

## Cách mở và gỡ lỗi
- **Cách mở nhanh**: Nhấn vào biểu tượng con tôm trên thanh menu và chọn **"Open Chat"**.
- **Xem nhật ký**: Nếu cửa sổ chat không hiện nội dung, hãy kiểm tra nhật ký bằng lệnh:
  `./scripts/clawlog.sh --category WebChatSwiftUI`

## Bảo mật
Ở chế độ từ xa, ứng dụng chỉ chuyển tiếp duy nhất cổng WebSocket cần thiết cho việc trao đổi dữ liệu chat, đảm bảo an toàn cho máy chủ của bạn.

---
Tài liệu liên quan: [Điều khiển từ xa](./remote.vi.md), [Cấu hình Gateway](../../gateway/configuration.vi.md).
