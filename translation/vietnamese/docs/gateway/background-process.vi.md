---
summary: "Thực thi ngầm và quản lý tiến trình của Agent"
read_when:
  - Bạn muốn tìm hiểu cách Agent quản lý các tiến trình chạy dài ngày hoặc chạy ngầm
---

# Thực thi ngầm & Công cụ quản lý tiến trình

Moltbot thực hiện các lệnh shell thông qua công cụ `exec` và giữ các tác vụ chạy dài trong bộ nhớ. Công cụ `process` được dùng để quản lý các phiên làm việc chạy ngầm đó.

## Công cụ `exec`

Các tham số chính:
- `command`: Lệnh cần thực thi.
- `yieldMs` (Mặc định 10.000): Tự động đẩy vào chế độ chạy ngầm sau khoảng thời gian này nếu lệnh chưa kết thúc.
- `background`: (Bolean) Đẩy vào chế độ chạy ngầm ngay lập tức.
- `timeout`: (Giây, mặc định 1800) Tự động ngắt tiến trình sau khoảng thời gian này.

Hành vi:
- Các lệnh chạy nhanh sẽ trả về kết quả trực tiếp trong ô chat.
- Khi được chạy ngầm, công cụ trả về trạng thái `running` kèm theo một `sessionId`.
- Đầu ra của lệnh được giữ trong bộ nhớ cho đến khi Agent truy vấn hoặc xóa bỏ.

## Cầu nối cho tiến trình con

Khi khởi tạo các tiến trình con bên ngoài các công cụ tiêu chuẩn, Moltbot sử dụng một "cầu nối" để đảm bảo các tín hiệu kết thúc được truyền đạt đầy đủ, tránh để lại các tiến trình "mồ côi" (zombie processes) chiếm dụng tài nguyên hệ thống.

## Công cụ `process`

Các hành động khả dụng:
- `list`: Liệt kê các phiên đang chạy và đã kết thúc.
- `poll`: Lấy dữ liệu đầu ra mới của một phiên (đồng thời báo cáo trạng thái kết thúc).
- `log`: Đọc toàn bộ lịch sử đầu ra của phiên.
- `write`: Gửi dữ liệu vào đầu vào tiêu chuẩn (stdin) của tiến trình (ví dụ: nhấn "y" để đồng ý).
- `kill`: Chấm dứt một phiên chạy ngầm.
- `clear`: Xóa một phiên đã kết thúc khỏi bộ nhớ.

---
Tài liệu liên quan: [Cấu hình hệ thống](./configuration.vi.md), [Xử lý lỗi](./troubleshooting.vi.md).
