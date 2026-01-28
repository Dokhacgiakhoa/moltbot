---
summary: "Cú pháp cho lệnh `/think` và `/verbose`, cách chúng ảnh hưởng đến quá trình suy nghĩ của AI"
read_when:
  - Bạn muốn điều chỉnh mức độ phân tích chuyên sâu của AI
---
# Các mức độ suy nghĩ (`/think`)

## Chức năng là gì?
AI hiện đại (như GPT-5.2) hỗ trợ khả năng "suy nghĩ" trước khi trả lời. Bạn có thể điều chỉnh mức độ này bằng các lệnh chỉ dẫn:
- `/think <mức_độ>` hoặc tắt bằng `/think off`.
- Các mức độ phổ biến: `minimal` (suy nghĩ nhanh), `low`, `medium`, `high` (suy nghĩ cực sâu - tốn nhiều token hơn).

## Cách thiết lập
1. **Theo từng tin nhắn**: Đặt lệnh `/think high` vào trong tin nhắn của bạn. AI sẽ chỉ suy nghĩ sâu cho riêng câu hỏi đó.
2. **Cho toàn bộ phiên làm việc**: Gửi một tin nhắn chỉ chứa `/think high`. AI sẽ duy trì mức độ này cho đến khi bạn đổi lại hoặc hết phiên làm việc.

## Chế độ hiển thị chi tiết (`/verbose`)
Lệnh này giúp bạn "nhìn thấu" quá trình làm việc của AI:
- `/verbose on`: AI sẽ thông báo mỗi khi nó bắt đầu sử dụng một công cụ (ví dụ: "Đang tìm kiếm web...", "Đang đọc file...").
- `/verbose full`: AI sẽ hiển thị cả kết quả đầu ra của các công cụ đó.
Đây là công cụ tuyệt vời để gỡ lỗi hoặc khi bạn muốn theo dõi sát sao AI đang làm gì.

## Hiển thị luồng suy nghĩ (`/reasoning`)
Với một số mô hình, bạn có thể yêu cầu AI hiển thị các khối suy nghĩ (Thinking blocks) trong câu trả lời bằng lệnh `/reasoning on`. Các suy nghĩ này thường được tách thành một tin nhắn riêng hoặc nằm trong khung ẩn để không làm rối câu trả lời chính.

---
Tài liệu liên quan: [Lệnh dấu gạch chéo](./slash-commands.vi.md), [Chế độ đặc quyền](./elevated.vi.md).
