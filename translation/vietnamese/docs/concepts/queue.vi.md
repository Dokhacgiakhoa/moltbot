---
summary: "Thiết kế hàng đợi lệnh giúp thực thi các phản hồi tự động theo tuần tự"
read_when:
  - Bạn muốn tìm hiểu về cơ chế xử lý đồng thời của Agent
---

# Hàng đợi lệnh (Command Queue)

Moltbot thực hiện tuần tự hóa các lượt chạy phản hồi tự động thông qua một hàng đợi nội bộ nhỏ. Điều này giúp ngăn chặn việc nhiều lượt chạy của Agent bị xung đột khi có nhiều tin nhắn đến cùng lúc, đồng thời vẫn cho phép thực hiện song song giữa các phiên làm việc khác nhau.

## Tại sao cần hàng đợi?
- Việc gọi AI (LLM) có thể tốn kém và gây xung đột nếu nhiều tin nhắn đến quá gần nhau.
- Xử lý tuần tự giúp tránh việc tranh chấp tài nguyên chung (tệp bộ nhớ, nhật ký) và giảm khả năng bị nhà cung cấp API giới hạn băng thông (rate limit).

## Cách thức hoạt động
- Hệ thống chia thành các **"luồng" (lanes)**. Mỗi phiên làm việc (`session`) có một luồng riêng, đảm bảo tại một thời điểm chỉ có một yêu cầu được xử lý cho một cuộc trò chuyện.
- Tất cả các luồng này được gom vào một **luồng tổng** để giới hạn số lượng xử lý đồng thời trên toàn hệ thống (mặc định cấu hình qua `maxConcurrent`).
- Các thông báo "đang soạn thảo" (typing indicators) vẫn sẽ được gửi đi ngay lập tức khi tin nhắn vào hàng đợi để người dùng không cảm thấy Bot bị chậm.

## Các chế độ hàng đợi (Queue Modes)
Bạn có thể điều chỉnh cách Bot xử lý khi tin nhắn mới đến trong lúc nó đang bận:

- **`collect` (Mặc định)**: Gom tất cả tin nhắn mới gửi đến thành **một lượt trả lời duy nhất** sau khi Bot rảnh.
- **`steer`**: Chèn tin nhắn mới trực tiếp vào lượt chạy hiện tại (Bot sẽ thay đổi nội dung đang trả lời dựa trên thông tin mới).
- **`followup`**: Tin nhắn sau sẽ được xếp hàng để trả lời ngay sau khi tin nhắn trước kết thúc.
- **`interrupt`**: Ngắt ngay lập tức câu trả lời hiện tại để xử lý tin nhắn mới.

## Cấu hình
Bạn có thể cấu hình toàn cục hoặc cho từng kênh chat trong phần `messages.queue`:

```json
{
  "messages": {
    "queue": {
      "mode": "collect",
      "debounceMs": 1000,
      "cap": 20
    }
  }
}
```

- `debounceMs`: Thời gian chờ "yên tĩnh" trước khi bắt đầu trả lời tin nhắn tiếp nối (tránh việc Bot bị "nói lắp").
- `cap`: Số lượng tin nhắn tối đa được phép xếp hàng cho một phiên làm việc.

---
Tài liệu liên quan: [Cấu hình hệ thống](../../gateway/configuration.vi.md), [Truyền tin (Streaming)](./streaming.vi.md).
