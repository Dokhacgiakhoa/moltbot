---
summary: "Sử dụng các mô hình ưu tiên quyền riêng tư của Venice AI trong Moltbot"
read_when:
  - Bạn muốn bảo vệ dữ liệu cá nhân khi trò chuyện với AI
  - Bạn cần cấu hình Venice AI trong Moltbot
---
# Venice AI (Tâm điểm Venius)

**Venius** là cấu hình đặc trưng của chúng tôi dành cho Venice AI - một nền tảng ưu tiên quyền riêng tư hàng đầu. Venice hỗ trợ các mô hình "không kiểm duyệt" (uncensored) và cung cấp quyền truy cập ẩn danh vào các model hàng đầu thế giới.

## Tại sao nên chọn Venice trong Moltbot?
- **Hoàn toàn riêng tư**: Dữ liệu của bạn không được dùng để huấn luyện và không bị lưu nhật ký (logging) trên máy chủ.
- **Mô hình không kiểm duyệt**: AI sẽ trả lời mọi yêu cầu của bạn mà không bị rào cản nội dung.
- **Truy cập ẩn danh**: Bạn có thể dùng Claude Opus, GPT-4o, Gemini thông qua cổng ẩn danh của Venice để giấu danh tính cá nhân.

## Các chế độ quyền riêng tư
Venice cung cấp hai cấp độ bảo mật chính:
- **Riêng tư (Private)**: Các mô hình như Llama, Qwen, DeepSeek chạy trong môi trường hoàn toàn không lưu trữ.
- **Ẩn danh (Anonymized)**: Các mô hình mạnh nhất như Claude 3.5/4.5 sẽ được chuyển tiếp qua Venice để xóa sạch các thông tin nhận dạng trước khi gửi tới nhà cung cấp gốc (Anthropic, OpenAI).

## Thiết lập nhanh
1. **Lấy mã API Key**: Đăng ký tại [venice.ai](https://venice.ai) và tạo mã tại mục Settings.
2. **Cấu hình qua CLI**:
   ```bash
   moltbot onboard --auth-choice venice-api-key
   ```
3. **Kiểm tra**:
   ```bash
   moltbot chat --model venice/llama-3.3-70b "Chào bạn!"
   ```

## Các lựa chọn mô hình khuyên dùng:
- **Toàn diện nhất**: `venice/llama-3.3-70b` (Mạnh mẽ, hoàn toàn riêng tư).
- **Thông minh nhất**: `venice/claude-opus-45` (Sử dụng qua cổng ẩn danh).
- **Lập trình**: `venice/qwen3-coder-480b` (Tối ưu cho code, ngữ cảnh cực rộng).
- **Tự do nhất**: `venice/venice-uncensored` (Không giới hạn nội dung).

## Lưu ý về chi phí
Venice sử dụng hệ thống V-Credits. Các mô hình "Private" thường có giá rẻ hơn các mô hình "Anonymized". Bạn có thể kiểm tra số dư và giá cước tại trang chủ của Venice AI.

---
Tài liệu liên quan: [Cấu hình Gateway](../gateway/configuration.vi.md), [Bảo mật](../gateway/security/index.vi.md).
