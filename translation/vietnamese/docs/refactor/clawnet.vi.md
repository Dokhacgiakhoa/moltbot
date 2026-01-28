---
summary: "Tái cấu trúc Clawnet: Thống nhất giao thức mạng, vai trò, xác thực, phê duyệt và danh tính"
---

# Tái cấu trúc Clawnet (Thống nhất Giao thức & Xác thực)

## Mục đích
Tài liệu này mô tả kế hoạch thống nhất các giao thức kết nối trong hệ thống Moltbot để đạt được:
- Một giao thức duy nhất cho toàn bộ các loại thiết bị (macOS, iOS, Android, CLI).
- Mọi thành viên trong mạng lưới đều được xác thực và ghép nối (pairing).
- Phân biệt rõ ràng vai trò giữa Nút mạng (Node) và Người điều khiển (Operator).
- Hệ thống phê duyệt tập trung, hiển thị thông báo ngay tại nơi người dùng đang sử dụng.
- Mã hóa dữ liệu bằng TLS cho toàn bộ lưu lượng mạng từ xa.

## Các vấn đề hiện tại
- Phải duy trì hai bộ giao thức khác nhau (WebSocket cho điều khiển và Bridge cho các nút mạng).
- Việc phê duyệt các lệnh hệ thống hiện đang hiển thị trên máy tính chạy lệnh, thay vì hiển thị trên điện thoại/máy tính mà người dùng đang cầm trên tay.
- Việc xác định danh tính thiết bị còn chồng chéo, một máy tính có thể hiện ra thành nhiều mục khác nhau trên giao diện.

## Trạng thái mới (Clawnet)

### Một giao thức, hai vai trò
Sử dụng một giao thức WebSocket duy nhất với các vai trò:
1. **Vai trò Nút mạng (Node)**: Cung cấp các khả năng như chụp ảnh, quay màn hình, chạy lệnh hệ thống. Không có quyền thay đổi cài đặt của Bot.
2. **Vai trò Người điều khiển (Operator)**: Có toàn quyền điều khiển Bot, thay đổi cấu hình, gửi tin nhắn và nhận các yêu cầu phê duyệt từ các nút mạng.

### Xác thực và Ghép nối thống nhất
- Mỗi thiết bị sẽ có một ID duy nhất dựa trên khóa bảo mật của nó.
- Khi một thiết bị mới kết nối, người dùng sẽ nhận được một yêu cầu ghép nối trên điện thoại/máy tính của mình để phê duyệt hoặc từ chối.

### Hệ thống phê duyệt tập trung
Thay vì hiển thị cửa sổ xác nhận trên máy tính chạy lệnh, thông báo sẽ được gửi tới tất cả các thiết bị "Người điều khiển" của bạn (ví dụ: iPhone của bạn). Bạn có thể bấm "Đồng ý" ngay trên điện thoại để máy tính ở nhà thực thi lệnh.

## Lộ trình thực hiện
- **Giai đoạn 1**: Thêm các vai trò và quyền hạn vào giao thức WebSocket hiện tại.
- **Giai đoạn 2**: Hỗ trợ song song cả giao thức cũ và mới để đảm bảo tính ổn định.
- **Giai đoạn 3**: Chuyển toàn bộ hệ thống phê duyệt sang kiểu tập trung.
- **Giai đoạn 4**: Mã hóa toàn bộ các kết nối bằng TLS.
- **Giai đoạn 5**: Gỡ bỏ hoàn toàn giao thức Bridge cũ.

---
Tài liệu liên quan: [Giao thức Gateway](../../gateway/protocol.vi.md), [Bảo mật Gateway](../../gateway/security.vi.md).
