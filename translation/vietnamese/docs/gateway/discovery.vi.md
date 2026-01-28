---
summary: "Khám phá Node và các phương thức truyền tải (Bonjour, Tailscale, SSH) để tìm thấy Gateway"
read_when:
  - Bạn muốn thay đổi cách các thiết bị (như Mac/iOS) tìm thấy máy chủ Gateway
---

# Khám phá & Phương thức truyền tải

Moltbot giải quyết hai vấn đề kết nối tương tự nhau:
1) **Điều khiển từ xa**: Ứng dụng Mac điều khiển một Gateway đang chạy ở nơi khác.
2) **Ghép nối thiết bị (Node)**: Ứng dụng iOS/Android tìm thấy Gateway và ghép nối an toàn.

## Các thuật ngữ chính

- **Gateway**: Tiến trình cốt lõi quản lý trạng thái, phiên làm việc và các kênh chat.
- **Gateway WebSocket (Control Plane)**: Cổng giao tiếp mặc định là `18789`.
- **Truyền tải trực tiếp (Direct)**: Kết nối qua mạng LAN hoặc Tailscale (Không dùng SSH).
- **Truyền tải qua SSH**: Phương án dự phòng vạn năng bằng cách chuyển tiếp cổng qua SSH.

## Tại sao cần cả hai phương thức "Trực tiếp" và "SSH"?

- **Kết nối trực tiếp** mang lại trải nghiệm tốt nhất trong mạng nội bộ:
  - Tự động tìm thấy nhau qua Bonjour.
  - Không cần quyền truy cập vào Shell máy chủ.
- **SSH** là phương án dự phòng luôn hoạt động:
  - Hoạt động ở bất cứ đâu có quyền SSH (ngay cả trên các mạng khác nhau).
  - Không cần mở thêm cổng mới trên tường lửa.

## Các cách để thiết bị tìm thấy Gateway

### 1) Bonjour / mDNS (Chỉ dành cho mạng nội bộ)
Đây là phương thức tiện lợi nhất trong cùng một mạng LAN. Gateway sẽ phát tín hiệu "tôi đang ở đây", và các thiết bị khách sẽ liệt kê danh sách để bạn chọn.

### 2) Tailscale (Xuyên mạng)
Đối với các thiết bị ở xa (ví dụ: điện thoại ở ngoài đường kết nối về máy tính ở nhà), Tailscale là phương thức khuyên dùng nhất. Sử dụng tên MagicDNS hoặc địa chỉ IP Tailscale để kết nối trực tiếp và an toàn.

### 3) Kết nối thủ công / SSH
Khi không thể kết nối trực tiếp, bạn luôn có thể nhập địa chỉ IP thủ công hoặc cấu hình SSH để "bắc cầu" kết nối.

## Trình tự ưu tiên kết nối (Client Policy)
Ứng dụng khách sẽ tự động thử kết nối theo thứ tự:
1. Thử địa chỉ đã từng ghép nối thành công trước đó.
2. Nếu trong mạng LAN, tìm kiếm qua Bonjour.
3. Thử qua địa chỉ Tailscale (nếu có).
4. Cuối cùng, dùng phương thức SSH.

---
Tài liệu liên quan: [Cấu hình Bonjour](./bonjour.vi.md), [Ghép nối thiết bị](./pairing.vi.md), [Truy cập từ xa](./remote.vi.md).
