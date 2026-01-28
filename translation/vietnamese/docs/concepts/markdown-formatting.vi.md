---
summary: "Quy trình xử lý định dạng Markdown cho các kênh nhắn tin đầu ra"
read_when:
  - Bạn đang thay đổi cách định dạng hoặc cắt nhỏ tin nhắn cho các kênh nhắn tin
  - Bạn muốn thêm một nhà cung cấp định dạng mới cho một kênh chat
---

# Định dạng Markdown

Moltbot định dạng các nội dung Markdown đầu ra bằng cách chuyển đổi chúng thành một **cấu trúc dữ liệu trung gian (IR)** chung trước khi kết xuất (render) ra định dạng đặc thù của từng kênh. Cách tiếp cận này giúp giữ nguyên nội dung văn bản gốc trong khi vẫn mang theo các thông tin về phong cách và liên kết, giúp việc cắt nhỏ tin nhắn (chunking) được nhất quán trên mọi nền tảng.

## Mục tiêu

- **Tính nhất quán**: Chỉ cần một bước phân tích cú pháp nhưng có thể dùng cho nhiều bộ kết xuất khác nhau.
- **Cắt nhỏ an toàn**: Chia văn bản thành các đoạn nhỏ trước khi kết xuất để đảm bảo các định dạng (như in đậm, in nghiêng) không bị lỗi khi nằm giữa các đoạn.
- **Phù hợp với từng kênh**: Chuyển đổi cùng một cấu trúc IR sang định dạng mrkdwn của Slack, HTML của Telegram hay các phạm vi phong cách của Signal mà không cần phân tích lại Markdown.

## Quy trình (Pipeline)

1. **Phân tích Markdown thành IR**:
   - IR bao gồm văn bản thuần túy kèm các vùng phong cách (bold, italic, strike, code, spoiler) và các liên kết.
   - Các bảng (tables) chỉ được phân tích khi kênh chat đó hỗ trợ chuyển đổi bảng.
2. **Cắt nhỏ IR (Ưu tiên định dạng)**:
   - Các vùng định dạng (như in đậm) sẽ được xử lý sao cho không bị ngắt giữa chừng khi chia tin nhắn.
3. **Kết xuất theo từng kênh**:
   - **Slack**: Dùng thẻ mrkdwn (ví dụ: `<url|label>`).
   - **Telegram**: Dùng thẻ HTML (ví dụ: `<b>`, `<i>`, `<a href>`).
   - **Signal**: Văn bản thuần kèm các dải phong cách; liên kết được chuyển thành dạng `nhãn (url)`.

## Xử lý bảng (Tables)

Do các bảng Markdown không được hỗ trợ nhất quán trên mọi nền tảng chat, Moltbot cung cấp các chế độ chuyển đổi qua tham số `markdown.tables`:

- `code` (Mặc định): Hiển thị bảng dạng khối mã nguồn (thường dùng cho Slack, Discord).
- `bullets`: Chuyển đổi mỗi hàng trong bảng thành một danh sách gạch đầu dòng (thường dùng cho WhatsApp, Signal).
- `off`: Giữ nguyên văn bản bảng thô.

## Lưu ý về liên kết

- **Slack**: `[nhãn](url)` trở thành `<url|nhãn>`. Các URL trần sẽ được giữ nguyên.
- **Telegram**: `[nhãn](url)` trở thành `<a href="url">nhãn</a>` (Chế độ HTML).
- **Signal**: `[nhãn](url)` trở thành `nhãn (url)` trừ khi nhãn trùng với URL.

---
Tài liệu liên quan: [Cắt nhỏ & Truyền tin](./streaming.vi.md), [Cấu hình hệ thống](../../gateway/configuration.vi.md).
