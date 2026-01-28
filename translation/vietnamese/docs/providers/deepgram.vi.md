---
summary: "Dịch vụ chuyển đổi giọng nói thành văn bản Deepgram cho các tin nhắn thoại"
read_when:
  - Bạn muốn AI có thể hiểu được nội dung của các tin nhắn thoại (voice notes)
---
# Deepgram (Chuyển đổi âm thanh)

Deepgram là một dịch vụ cung cấp API chuyển đổi giọng nói thành văn bản (Speech-to-Text). Trong Moltbot, nó được sử dụng để **xử lý các tin nhắn thoại gửi tới bot**.

Khi được kích hoạt, Moltbot sẽ tải tệp âm thanh lên Deepgram và đưa nội dung văn bản thu được vào luồng xử lý của AI. AI sẽ nhìn thấy nội dung tin nhắn thoại giống như một tin nhắn văn bản thông thường.

## Khởi động nhanh

1. **Lấy API Key**: Đăng ký tại [deepgram.com](https://deepgram.com) để nhận mã.
2. **Thiết lập biến môi trường**:
   ```
   DEEPGRAM_API_KEY=dg_...
   ```
3. **Bật trong file cấu hình**:
   ```json5
   {
     tools: {
       media: {
         audio: {
           enabled: true,
           models: [{ provider: "deepgram", model: "nova-3" }]
         }
       }
     }
   }
   ```

## Các tùy chọn nâng cao
Bạn có thể cấu hình thêm các tính năng như:
- `language`: Chỉ định ngôn ngữ (ví dụ: `vi` cho tiếng Việt).
- `detect_language`: Tự động nhận diện ngôn ngữ.
- `punctuate`: Tự động thêm dấu câu.
- `smart_format`: Định dạng văn bản thông minh (ngày tháng, đơn vị tiền tệ...).

## Lưu ý
- Deepgram nổi tiếng với tốc độ xử lý nhanh và độ chính xác cao, đặc biệt là với model `nova-3`.
- Chi phí sẽ được tính dựa trên số phút âm thanh mà bạn chuyển đổi qua tài khoản Deepgram của mình.

---
Tài liệu liên quan: [Cấu hình Gateway](../gateway/configuration.vi.md), [Xử lý đa phương tiện](../../concepts/media.vi.md).
