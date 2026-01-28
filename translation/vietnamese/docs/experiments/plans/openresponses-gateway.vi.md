---
summary: "Kế hoạch: Thêm điểm cuối OpenResponses /v1/responses và dọn dẹp các điểm cuối cũ"
owner: "moltbot"
status: "bản thảo"
last_updated: "2026-01-19"
---

# Kế hoạch tích hợp Gateway OpenResponses

## Bối cảnh
Moltbot Gateway hiện đang cung cấp một API tương thích tối thiểu với OpenAI tại `/v1/chat/completions`. Tuy nhiên, chúng tôi muốn chuyển sang chuẩn **Open Responses** — một tiêu chuẩn mở mới được thiết kế riêng cho các tác vụ của Agent (AI Agent) với khả năng xử lý các sự kiện theo luồng một cách thông minh hơn.

## Mục tiêu
- Thêm điểm cuối `/v1/responses` tuân theo tiêu chuẩn OpenResponses.
- Duy trì điểm cuối Chat Completions cũ cho đến khi hoàn toàn ổn định để có thể gỡ bỏ sau này.
- Chuẩn hóa việc kiểm tra và phân tích dữ liệu bằng các sơ đồ (schemas) độc lập.

## Kiến trúc đề xuất
- Thêm tệp cấu trúc dữ liệu `open-responses.schema.ts` (sử dụng Zod).
- Thêm điểm cuối `/v1/responses` trong khi vẫn giữ nguyên `/v1/chat/completions` như một lớp tương thích cũ.
- Cho phép bật/tắt từng điểm cuối này trong phần cài đặt Gateway.
- Hiển thị cảnh báo khi khởi động nếu người dùng vẫn sử dụng điểm cuối Chat Completions cũ.

## Các giai đoạn hỗ trợ (Giai đoạn 1)
- Chấp nhận dữ liệu vào dưới dạng văn bản hoặc mảng các tin nhắn (messages).
- Hỗ trợ các vai trò: `system`, `developer`, `user`, `assistant`.
- Chưa hỗ trợ xử lý hình ảnh hoặc tệp tin trong giai đoạn này.
- Trả về câu trả lời kèm theo thông tin về lượng tài nguyên đã sử dụng (usage).

## Chiến lược xác thực
- Sử dụng thư viện Zod để kiểm tra tính hợp lệ của dữ liệu mà không cần SDK bên ngoài.
- Đảm bảo dữ liệu đầu vào và đầu ra tuân thủ nghiêm ngặt tiêu chuẩn OpenResponses để dễ dàng mở rộng sau này.

---
Tài liệu liên quan: [Cấu hình Gateway](../../gateway/configuration.vi.md), [API HTTP kiểu OpenAI](../../gateway/openai-http-api.vi.md).
