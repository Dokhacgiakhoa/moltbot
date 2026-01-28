---
summary: "Giao diện dòng lệnh (TUI): Kết nối tới Gateway từ bất kỳ máy tính nào"
---

# Giao diện dòng lệnh (TUI)

## Bắt đầu nhanh

1. Khởi động Gateway:
   `moltbot gateway`
2. Mở giao diện TUI:
   `moltbot tui`
3. Nhập tin nhắn và nhấn Enter.

**Kết nối tới Gateway từ xa:**
`moltbot tui --url ws://<địa_chỉ>:<cổng> --token <mã_token>`

## Giao diện hiển thị

- **Tiêu đề**: URL kết nối, Agent hiện tại, và phiên làm việc hiện tại.
- **Nhật ký trò chuyện**: Tin nhắn của bạn, phản hồi của trợ lý, thông báo hệ thống và thẻ công cụ.
- **Thanh trạng thái**: Trạng thái kết nối/chạy (đang kết nối, đang chạy, đang truyền phát, nghỉ, lỗi).
- **Chân trang**: Thông tin chi tiết về Agent, phiên, mô hình, mức độ suy luận và số Token đã dùng.
- **Ô nhập liệu**: Trình soạn thảo văn bản hỗ trợ tự động hoàn thành (autocomplete).

## Quản lý Session & Agents

- **Agents**: Là các định danh duy nhất (ví dụ: `main`, `research`).
- **Sessions**: Thuộc về Agent hiện tại.
- Bạn có thể dùng lệnh `/session [tên]` để chuyển đổi phiên làm việc của Agent hiện tại.
- Phân loại phiên:
  - `per-sender` (mặc định): Mỗi người gửi có nhiều phiên riêng.
  - `global`: Dùng chung một phiên duy nhất.

## Phím tắt bàn phím

- **Enter**: Gửi tin nhắn.
- **Esc**: Hủy yêu cầu đang chạy.
- **Ctrl+C**: Xóa ô nhập liệu (nhấn 2 lần để thoát).
- **Ctrl+D**: Thoát.
- **Ctrl+L**: Bảng chọn mô hình (Model picker).
- **Ctrl+G**: Bảng chọn Agent (Agent picker).
- **Ctrl+P**: Bảng chọn phiên (Session picker).
- **Ctrl+O**: Bật/tắt hiển thị chi tiết kết quả công cụ.

## Các lệnh điều khiển (Slash Commands)

- `/help`: Trợ giúp.
- `/status`: Kiểm tra trạng thái.
- `/new` hoặc `/reset`: Làm mới phiên làm việc.
- `/deliver on|off`: Bật/tắt việc gửi câu trả lời tới nhà cung cấp tin nhắn (mặc định là tắt trong TUI).
- `/think [mức độ]`: Chỉnh mức độ suy luận (thinking).
- `/usage [chế độ]`: Chỉnh hiển thị mức dùng Token.

## Chạy lệnh hệ thống cục bộ

Bạn có thể chạy lệnh của máy tính đang mở TUI bằng cách thêm dấu `!` vào đầu dòng. Ví dụ: `!ls -la`.

---
Tài liệu liên quan: [Giao diện Web](../web/index.vi.md), [Hướng dẫn CLI](../cli/index.vi.md).
