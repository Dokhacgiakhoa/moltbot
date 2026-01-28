---
summary: "Nội dung câu lệnh hệ thống của Moltbot và cách nó được lắp ráp"
read_when:
  - Bạn muốn chỉnh sửa nội dung câu lệnh gốc gửi cho AI
---

# Câu lệnh hệ thống (System Prompt)

Moltbot xây dựng một câu lệnh hệ thống tùy chỉnh cho mỗi lượt chạy của Agent. Câu lệnh này **do Moltbot quản lý hoàn toàn** và được thiết kế để tối ưu hóa việc sử dụng công cụ cũng như hoạt động trong các kênh nhắn tin.

## Cấu trúc câu lệnh

Câu lệnh được thiết kế súc tích và chia thành các phần cố định:

- **Công cụ (Tooling)**: Danh sách các công cụ hiện có kèm mô tả ngắn.
- **Kỹ năng (Skills)**: Chỉ dẫn cho AI cách nạp hướng dẫn chi tiết của từng kỹ năng khi cần.
- **Tự cập nhật**: Cách AI có thể tự chạy lệnh nâng cấp hệ thống.
- **Không gian làm việc**: Thư mục làm việc hiện tại.
- **Thông tin Sandbox**: Cảnh báo nếu AI đang chạy trong môi trường bị cô lập (Docker).
- **Thời gian hiện tại**: Giờ địa phương của người dùng và múi giờ.
- **Ghi chú về nhịp tim (Heartbeats)**: Chỉ dẫn cho các lượt chạy tự động ngầm.
- **Thông tin hệ thống**: Hệ điều hành, phiên bản Node, mô hình AI đang dùng.

## Các chế độ câu lệnh (Prompt Modes)

Moltbot có thể tự động tinh giản câu lệnh cho các tình huống khác nhau:
- **`full` (Mặc định)**: Bao gồm tất cả các thành phần trên.
- **`minimal`**: Dùng cho các **Agent phụ (Sub-agents)**. Chế độ này lược bỏ các phần về kỹ năng, bộ nhớ dài hạn, và các quy tắc nhắn tin phức tạp để tiết kiệm Token và tăng tốc độ xử lý.

## Nạp tệp khởi tạo từ không gian làm việc

Các tệp quan trọng trong thư mục làm việc của bạn sẽ được "đọc trước" và đính kèm vào câu lệnh hệ thống để AI hiểu ngay lập tức về tính cách và nhiệm vụ của nó:

- `AGENTS.md`: Chỉ dẫn vận hành.
- `SOUL.md`: Tính cách và ranh giới.
- `USER.md`: Thông tin về bạn.
- `IDENTITY.md`: Tên và định danh của Agent.

Nếu tệp quá lớn, hệ thống sẽ tự động cắt bớt và đánh dấu bằng một ký hiệu đặc biệt. Bạn có thể dùng lệnh `/context list` để kiểm tra dung lượng của các tệp này trong câu lệnh hệ thống.

---
Tài liệu liên quan: [Cấu trúc Ngữ cảnh](./context.vi.md), [Kỹ năng AI](../../tools/skills.vi.md), [Xử lý ngày tháng](../../date-time.vi.md).
