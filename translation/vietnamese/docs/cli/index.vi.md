---
summary: "Tài liệu tham khảo lệnh CLI `moltbot`, các lệnh con và tùy chọn"
read_when:
  - Khi bạn cần tra cứu cách sử dụng các lệnh của Moltbot trong terminal
---

# Tài liệu tham khảo CLI

Trang này mô tả chi tiết các lệnh và hành vi của giao diện dòng lệnh (CLI). Nếu các lệnh có sự thay đổi, tài liệu này sẽ được cập nhật tương ứng.

## Danh mục lệnh chi tiết

Dưới đây là liên kết tới các trang chi tiết cho từng nhóm lệnh:

- [`setup`](./setup.vi.md): Khởi tạo cấu hình và không gian làm việc.
- [`onboard`](./onboard.vi.md): Trình thuật sĩ thiết lập nhanh hệ thống.
- [`configure`](./configure.vi.md): Trình thuật sĩ cấu hình (mô hình, kênh, kỹ năng).
- [`config`](./config.vi.md): Các lệnh hỗ trợ cấu hình không tương tác (get/set).
- [`doctor`](./doctor.vi.md): Kiểm tra sức khỏe và sửa lỗi nhanh.
- [`gateway`](./gateway.vi.md): Quản lý máy chủ cổng kết nối WebSocket.
- [`models`](./models.vi.md): Quản lý các mô hình AI và xác thực.
- [`channels`](./channels.vi.md): Quản lý các tài khoản kênh chat (WhatsApp, Telegram...).
- [`skills`](./skills.vi.md): Liệt kê và kiểm tra các kỹ năng khả dụng.
- [`status`](./status.vi.md): Hiển thị trạng thái hoạt động của hệ thống.
- [`logs`](./logs.vi.md): Xem nhật ký hoạt động từ Gateway.

## Các cờ (flags) toàn cục

- `--dev`: Cách ly dữ liệu trong thư mục `~/.clawdbot-dev` và sử dụng các cổng mặc định khác.
- `--profile <tên>`: Cách ly dữ liệu trong thư mục `~/.clawdbot-<tên>`.
- `--no-color`: Tắt màu sắc hiển thị trong terminal.
- `-V`, `--version`, `-v`: Hiển thị phiên bản hiện tại.

## Màu sắc hiển thị

Moltbot sử dụng bảng màu "tôm hùm" đặc trưng để giúp bạn dễ dàng đọc thông tin trong terminal:

- `accent` (#FF5A2D): Tiêu đề, nhãn, các điểm nhấn chính.
- `info` (#FF8A5B): Các giá trị thông tin.
- `success` (#2FBF71): Trạng thái thành công.
- `warn` (#FFB020): Cảnh báo, các phương án dự phòng.
- `error` (#E23D2D): Lỗi, thất bại.
- `muted` (#8B7F77): Thông tin nền, siêu dữ liệu.

## Cấu trúc cây lệnh (Tóm tắt)

```
moltbot [--dev] [--profile <tên>] <lệnh>
  setup          - Khởi tạo hệ thống
  onboard        - Thuật sĩ thiết lập
  configure      - Cấu hình tương tác
  config         - Quản lý file cấu hình
  doctor         - Chẩn đoán lỗi
  status         - Trạng thái hệ thống
  gateway        - Máy chủ WebSocket
  channels       - Kênh truyền thông
  models         - Mô hình AI
  skills         - Kỹ năng của Agent
  logs           - Xem nhật ký
```

---
Tài liệu liên quan: [Cấu hình hệ thống](../gateway/configuration.vi.md), [Hướng dẫn Onboarding](../../start/onboarding.vi.md).
