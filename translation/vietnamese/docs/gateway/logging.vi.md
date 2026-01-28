---
summary: "Hệ thống nhật ký: Nhật ký tệp, nội dung bảng điều khiển và định dạng hiển thị"
read_when:
  - Bạn muốn chẩn đoán lỗi sâu bên trong các thành phần của hệ thống
---

# Nhật ký hệ thống (Logging)

Moltbot có hai luồng nhật ký chính:
- **Nội dung bảng điều khiển (Console output)**: Những gì bạn nhìn thấy trực tiếp trong Terminal.
- **Nhật ký tệp (File logs)**: Các tệp tin được ghi lại vào ổ cứng để tra cứu sau này.

## Nhật ký tệp (File-based logger)
Theo mặc định, nhật ký được ghi vào thư mục `/tmp/moltbot/` với định dạng `moltbot-YYYY-MM-DD.log` (mỗi ngày một tệp). Bạn có thể chỉnh sửa vị trí và mức độ chi tiết trong tệp cấu hình:
- `logging.file`: Đường dẫn tệp.
- `logging.level`: Mức độ chi tiết (info, debug, trace).

Bạn có thể theo dõi nhật ký tệp này trong thời gian thực bằng lệnh:
```bash
moltbot logs --follow
```

## Điều chỉnh độ chi tiết
- **Mặc định**: Chỉ hiển thị các thông tin quan trọng.
- **Chế độ Verbose (`--verbose`)**: Hiển thị tất cả các lượt giao tiếp giữa Gateway và các thiết bị (handshakes, events). Đây là chế độ tốt nhất để tìm lỗi kết nối.

## Ẩn thông tin nhạy cảm
Moltbot tích hợp tính năng **Tool summary redaction**: Tự động lọc các từ khóa như mật khẩu, Khóa API, hay Token xác thực khỏi các dòng nhật ký hiển thị trên màn hình để tránh việc bạn vô tình để lộ bí mật khi chụp ảnh màn hình hoặc quay video.

---
Tài liệu liên quan: [Chẩn đoán lỗi](./doctor.vi.md), [Xử lý lỗi](./troubleshooting.vi.md).
