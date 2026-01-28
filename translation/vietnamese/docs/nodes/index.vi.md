---
summary: "Nút mạng (Nodes): Ghép nối, khả năng, quyền hạn và các công cụ hỗ trợ giao diện Canvas/Camera/Màn hình"
read_when:
  - Bạn muốn kết nối điện thoại hoặc máy tính phụ làm thiết bị ngoại vi cho Bot
  - Bạn muốn sử dụng khả năng "nhìn" và "điều khiển" của các thiết bị này
---

# Các Nút mạng (Nodes)

Một **Nút mạng (Node)** là một thiết bị đồng hành (macOS, iOS, Android hoặc máy chủ không giao diện) kết nối với Moltbot Gateway. Chúng đóng vai trò như các thiết bị ngoại vi, cung cấp các khả năng như hiển thị giao diện (Canvas), sử dụng Camera, quay màn hình hoặc chạy các lệnh hệ thống.

## Ghép nối và Trạng thái

Các thiết bị kết nối qua WebSocket cần được **ghép nối (pairing)** với Gateway. Khi một thiết bị mới kết nối, Gateway sẽ tạo một yêu cầu ghép nối. Bạn cần phê duyệt yêu cầu này qua dòng lệnh (CLI) hoặc giao diện điều khiển.

Các lệnh CLI nhanh:
```bash
moltbot devices list             # Liệt kê các yêu cầu ghép nối
moltbot devices approve <id>     # Phê duyệt thiết bị
moltbot nodes status             # Kiểm tra trạng thái các nút đang kết nối
```

## Các khả năng chính của Nút mạng

### 1. Hiển thị Canvas (Giao diện đồ họa)
Moltbot có thể hiển thị một trang web hoặc giao diện điều khiển trên màn hình của Nút mạng (điện thoại hoặc máy Mac).
- `canvas.present`: Hiển thị một URL hoặc trang web.
- `canvas.snapshot`: Chụp ảnh lại nội dung đang hiển thị trên giao diện đó.

### 2. Sử dụng Camera (Ảnh và Video)
Bot có thể yêu cầu chụp ảnh hoặc quay video từ các camera của thiết bị.
- `camera.snap`: Chụp ảnh từ camera trước/sau.
- `camera.clip`: Quay video ngắn (dưới 60 giây).

### 3. Quay màn hình
Hỗ trợ quay lại nội dung màn hình của thiết bị để AI có thể hiểu người dùng đang làm gì.
- `screen.record`: Quay video màn hình kèm âm thanh.

### 4. Vị trí Địa lý
Nếu được cho phép, Bot có thể lấy tọa độ hiện tại của thiết bị (Kinh độ/Vĩ độ).
- `location.get`: Lấy vị trí với độ chính xác tùy chọn.

### 5. Lệnh hệ thống (System commands)
Trên máy Mac hoặc các Nút mạng là máy chủ, Bot có thể chạy các lệnh đầu cuối (Terminal) thông qua `system.run`. Để đảm bảo an toàn, các lệnh này phải nằm trong **Danh sách cho phép (Allowlist)** mà bạn đã thiết lập.

---
Tài liệu liên quan: [Giao diện Canvas](./canvas.vi.md), [Sử dụng Camera](./camera.vi.md), [Quyền thực thi hệ thống](../../tools/exec-approvals.vi.md).
