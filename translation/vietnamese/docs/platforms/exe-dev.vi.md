---
summary: "Chạy Moltbot Gateway trên nền tảng exe.dev (Sử dụng máy ảo + HTTPS proxy tích hợp sẵn)"
read_when:
  - Bạn muốn có địa chỉ HTTPS công khai một cách nhanh chóng mà không cần cấu hình tên miền
---

# Moltbot trên exe.dev

**Mục tiêu**: Chạy Moltbot Gateway trên máy ảo của [exe.dev](https://exe.dev) và truy cập từ xa qua địa chỉ: `https://ten-may-ao.exe.xyz`.

## Cách cài đặt nhanh nhất (Dùng Shelley Agent)
Shelley là trợ lý AI của nền tảng exe.dev, bạn có thể ra lệnh cho nó cài đặt Moltbot chỉ bằng một câu lệnh:
> "Cài đặt Moltbot trên máy ảo này. Cấu hình nginx để chuyển tiếp từ cổng 18789 ra cổng công khai, hỗ trợ Websocket. Đảm bảo trạng thái sức khỏe của Bot là OK."

## Cài đặt thủ công
1. Tạo máy ảo mới: `ssh exe.dev new`.
2. Chạy kịch bản cài đặt Moltbot.
3. Cấu hình Nginx để làm cầu nối giữa cổng 18789 (nội bộ) và internet.
4. Truy cập qua địa chỉ HTTPS mà exe.dev cấp cho bạn.

## Ưu điểm của exe.dev
- **HTTPS sẵn có**: Bạn không phải loay hoay với SSL hay Cerbot.
- **Xác thực tích hợp**: Hệ thống đã có sẵn lớp bảo vệ bằng email trước khi vào được Bot của bạn.

---
Tài liệu liên quan: [Vận hành Gateway](../../gateway/index.vi.md), [Cài đặt](../../install/index.vi.md).
