---
summary: "Ứng dụng Android (Nút mạng): Quy trình kết nối + Canvas/Chat/Camera"
read_when:
  - Bạn đang ghép nối (pairing) hoặc kết nối lại thiết bị Android
  - Bạn cần xử lý lỗi tìm kiếm Gateway hoặc xác thực trên Android
---

# Ứng dụng Android (Nút mạng)

## Tóm tắt hỗ trợ
- **Vai trò**: Là một nút mạng đi kèm (Android không đóng vai trò làm Gateway).
- **Yêu cầu Gateway**: Có (Bạn phải chạy Gateway trên macOS, Linux hoặc Windows qua WSL2).
- **Cài đặt**: [Bắt đầu nhanh](../../start/getting-started.vi.md) + [Ghép nối](../../gateway/pairing.vi.md).

## Quy trình kết nối

Ứng dụng Android ⇄ (mDNS + WebSocket) ⇄ **Gateway**

Thiết bị Android kết nối trực tiếp đến Gateway qua WebSocket (mặc định là `ws://<ip-may-chu>:18789`) và sử dụng cơ chế ghép nối do Gateway quản lý.

### Các bước thực hiện

#### 1) Khởi động Gateway
Chạy lệnh sau trên máy tính chủ:
```bash
moltbot gateway --port 18789 --verbose
```
Đảm bảo thấy dòng nhật ký: `listening on ws://0.0.0.0:18789`.

#### 2) Kết nối từ ứng dụng Android
Trong ứng dụng trên điện thoại:
- Mở phần **Settings**.
- Tại mục **Discovered Gateways**, chọn máy chủ của bạn và nhấn **Connect**.
- Nếu không tìm thấy tự động, hãy dùng mục **Advanced → Manual Gateway** để nhập địa chỉ IP và cổng thủ công.

#### 3) Phê duyệt ghép nối (Trên máy tính)
Trên máy tính đang chạy Gateway, hãy chạy lệnh sau để đồng ý cho điện thoại kết nối:
```bash
moltbot nodes pending    # Xem danh sách yêu cầu đang chờ
moltbot nodes approve <requestId>    # Phê duyệt yêu cầu
```

#### 4) Kiểm tra trạng thái
```bash
moltbot nodes status
```

## Các tính năng đặc biệt

### Canvas + Camera
- **Canvas**: Cho phép hiển thị nội dung HTML/JS mà Agent có thể chỉnh sửa trực tiếp. Agent có thể dùng lệnh `canvas.navigate` để điều hướng màn hình điện thoại của bạn đến một trang web cụ thể.
- **Camera**: Agent có thể yêu cầu chụp ảnh (`camera.snap`) hoặc quay video ngắn (`camera.clip`) từ điện thoại của bạn sau khi được cấp quyền.

---
Tài liệu liên quan: [Ghép nối thiết bị](../../gateway/pairing.vi.md), [Tìm kiếm Bonjour](../../gateway/bonjour.vi.md).
