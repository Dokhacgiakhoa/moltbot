---
summary: "Tích hợp Telegram Bot API thông qua grammY kèm các lưu ý thiết lập"
read_when:
  - Khi bạn làm việc với kênh Telegram hoặc muốn hiểu cách thức kết nối grammY
---
# Tích hợp grammY (Telegram Bot API)

## Tại sao sử dụng grammY?
- Đây là một thư viện TypeScript mạnh mẽ cho Telegram Bot API, hỗ trợ đầy đủ các tính năng như long-poll, webhook, xử lý lỗi và giới hạn băng thông (rate limit).
- Hỗ trợ xử lý truyền thông (media) sạch sẽ hơn so với việc tự viết các lệnh gửi dữ liệu thủ công.
- Có khả năng mở rộng tốt, hỗ trợ Proxy và bảo mật kiểu dữ liệu (type-safe).

## Các tính năng đã triển khai
- **Cơ chế hoạt động**: grammY hiện là thư viện duy nhất được Moltbot sử dụng để gửi và nhận tin nhắn từ Telegram.
- **Chế độ kết nối**: Hỗ trợ cả `long-polling` (bot tự đi hỏi tin nhắn mới) và `webhooks` (Telegram tự đẩy tin nhắn tới bot). Chế độ webhook sẽ được bật nếu bạn cấu hình trường `webhookUrl`.
- **Hỗ trợ Proxy**: Bạn có thể thiết lập Proxy thông qua `channels.telegram.proxy` nếu gặp vấn đề về kết nối mạng.
- **Luồng tin nhắn (Streaming)**: Hỗ trợ chế độ truyền phát bản nháp (`sendMessageDraft`) trong các phòng chat riêng tư hoặc chủ đề (Topics) - yêu cầu Bot API 9.3+.
- **Cô lập phiên làm việc**: Các cuộc hội thoại cá nhân sẽ được đưa vào phiên làm việc chính, trong khi các nhóm chat sẽ có phiên làm việc riêng dựa trên `chatId` của nhóm.

---
Tài liệu liên quan: [Cấu hình Telegram](./telegram.vi.md).
