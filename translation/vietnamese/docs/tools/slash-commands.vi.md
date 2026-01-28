---
summary: "Các lệnh dấu gạch chéo (/): Văn bản so với gốc, cấu hình và danh sách các lệnh được hỗ trợ"
read_when:
  - Bạn muốn sử dụng hoặc cấu hình các câu lệnh trong ứng dụng chat
---
# Lệnh dấu gạch chéo (Slash commands)

Các câu lệnh được xử lý trực tiếp bởi Gateway. Hầu hết các lệnh phải được gửi dưới dạng một tin nhắn **riêng lẻ** bắt đầu bằng dấu `/`.

## Hai hệ thống lệnh chính:
- **Lệnh (Commands)**: Các tin nhắn đứng độc lập như `/help`, `/status`.
- **Lệnh điều hướng (Directives)**: Như `/think`, `/model`, `/elevated`.
  - Các lệnh này được loại bỏ khỏi tin nhắn trước khi AI nhìn thấy nội dung.
  - Nếu đi kèm trong một câu văn, chúng chỉ mang tính chất "gợi ý" cho tin nhắn đó mà không thay đổi cài đặt lâu dài.
  - Nếu gửi tin nhắn chỉ chứa lệnh điều hướng, cài đặt đó sẽ được lưu lại cho toàn bộ phiên làm việc.

## Danh sách các lệnh phổ biến:
- `/help`: Xem hướng dẫn sử dụng.
- `/status`: Kiểm tra trạng thái hệ thống và hạn mức sử dụng AI.
- `/new [tên_mô_hình]`: Bắt đầu một phiên trò chuyện mới (có thể chọn lại mô hình AI).
- `/think <mức_độ>`: Thay đổi mức độ "suy nghĩ" của AI (low, medium, high...).
- `/model <tên>`: Đổi sang một mô hình AI khác ngay lập tức.
- `/whoami`: Xem mã định danh (ID) của bạn trong hệ thống.
- `/stop`: Dừng lượt chạy hiện tại của AI.
- `/reset`: Xóa lịch sử trò chuyện và bắt đầu lại.

## Cấu hình
Bạn có thể bật hoặc tắt các loại lệnh khác nhau trong file cấu hình (`commands.text`, `commands.native`). Moltbot hỗ trợ tự động đăng ký các lệnh này như lệnh hệ thống trên Discord, Telegram và Slack (Native Commands) để bạn dễ dàng lựa chọn từ menu.

## Lưu lý về quyền hạn
Các lệnh nhạy cảm như `/config` (sửa cấu hình hệ thống) hoặc `/elevated` (nâng quyền thực thi) chỉ dành cho người quản lý hoặc những người được ủy quyền trong danh sách trắng.

---
Tài liệu liên quan: [Chế độ đặc quyền](./elevated.vi.md), [Quản lý hàng đợi](../concepts/queue.vi.md).
