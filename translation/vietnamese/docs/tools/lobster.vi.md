---
summary: "Trình thực thi quy trình công việc Lobster cho Moltbot với các điểm phê duyệt có thể tạm dừng."
read_when:
  - Bạn muốn AI thực hiện các quy trình nhiều bước một cách chắc chắn và có kiểm soát
  - Cần tạm dừng quy trình để người dùng phê duyệt trước khi đi tiếp
---
# Lobster (Quy trình công việc thông minh)

Lobster là một hệ thống cho phép Moltbot thực hiện một chuỗi nhiều thao tác liên tiếp như một quy trình duy nhất, an toàn và có các điểm chốt để bạn phê duyệt.

## Tại sao bạn cần Lobster?
Thông thường, các công việc phức tạp yêu cầu AI phải gọi lệnh qua lại rất nhiều lượt. Mỗi lượt như vậy đều tốn chi phí và AI có thể bị "lạc lối" giữa chừng. Lobster giải quyết vấn đề này:
- **Gộp nhiều bước thành một**: AI chỉ cần gọi một quy trình Lobster và nhận về kết quả duy nhất.
- **Phê duyệt tích hợp**: Các bước nhạy cảm (như gửi email, xóa file) sẽ tạm dừng quy trình và hỏi ý kiến bạn.
- **Có thể tiếp tục**: Nếu quy trình bị tạm dừng, nó sẽ trả về một "mã thông báo" (token). Bạn chỉ cần đồng ý và AI sẽ tiếp tục từ nơi nó dừng lại mà không phải chạy lại từ đầu.

## Cách thức hoạt động
Hãy tưởng tượng một quy trình xử lý hòm thư:
1. Liệt kê các email mới.
2. Phân loại email.
3. Dự thảo câu trả lời.
4. **Tạm dừng: Bạn nhấn "Đồng ý" trên điện thoại.**
5. Gửi các email đã dự thảo.

AI sẽ khởi chạy quy trình này, và Lobster sẽ đảm bảo các bước diễn ra đúng trình tự. Nếu bạn không đồng ý ở bước 4, các email sẽ không bao giờ được gửi đi.

## Đặc điểm kỹ thuật
- **Tính xác định**: Quy trình chạy theo một kịch bản định sẵn, giúp bạn dễ dàng kiểm soát và dự đoán kết quả.
- **An toàn Tuyệt đối**: Các quy trình Lobster luôn tuân thủ các quy tắc bảo mật và thời gian chờ (timeouts) của hệ thống.
- **Dễ dàng mở rộng**: Bạn có thể tự viết các kịch bản `.lobster` cho riêng mình bằng ngôn ngữ đơn giản.

---
Tài liệu liên quan: [Tác vụ LLM JSON](./llm-task.vi.md), [Phê duyệt thực thi lệnh](./exec-approvals.vi.md), [Plugin](../../plugin.vi.md).
