---
summary: "Tính năng hiểu nội dung hình ảnh/âm thanh/video đầu vào với cơ chế tự động chuyển đổi"
read_when:
  - Bạn muốn Bot tự động tóm tắt nội dung các tệp bạn gửi trước khi trả lời
---

# Hiểu phương tiện truyền thông (Đầu vào)

Moltbot có khả năng **tóm tắt nội dung các phương tiện truyền thông** (hình ảnh/âm thanh/video) mà bạn gửi đến trước khi Bot xử lý câu trả lời. Tính năng này giúp Bot nắm bắt bối cảnh nhanh hơn và xử lý các lệnh từ xa (như tin nhắn thoại) hiệu quả hơn.

## Cách hoạt động
1. Bot nhận tệp đính kèm (Hình ảnh, m thanh hoặc Video).
2. Bot chọn công cụ phù hợp nhất (Mô hình AI hoặc ứng dụng tại máy) dựa trên dung lượng và loại tệp.
3. Bot thực hiện phân tích tệp.
4. Sau khi thành công:
   - Nội dung hội thoại sẽ được thêm các đoạn mô tả như `[Image]`, `[Audio]` hoặc `[Video]`.
   - Đối với âm thanh, văn bản chuyển đổi (transcript) sẽ được dùng để Bot hiểu ý nghĩa câu nói của bạn.

Nếu quá trình phân tích thất bại hoặc bị tắt, Bot vẫn sẽ nhận được tệp gốc và xử lý như bình thường.

## Tự động phát hiện (Mặc định)
Nếu bạn không cài đặt cụ thể, Moltbot sẽ tự tìm công cụ chuyển đổi theo thứ tự:
1. **Công cụ tại máy (CLI)**: Ưu tiên whisper cho âm thanh.
2. **Gemini CLI**: Sử dụng lệnh `gemini` để đọc tệp.
3. **Các khóa API**: Sử dụng OpenAI, Anthropic, Google hoặc Deepgram nếu bạn có sẵn khóa API.

## Giới hạn mặc định
- **Hình ảnh/Video**: Tóm tắt ngắn gọn trong khoảng **500 ký tự** để tiết kiệm tài nguyên.
- **m thanh**: Chuyển đổi toàn bộ nội dung thành văn bản.
- **Dung lượng tối đa**: Ảnh (10MB), m thanh (20MB), Video (50MB). Nếu vượt quá, Bot sẽ bỏ qua việc tóm tắt và gửi thẳng tệp gốc cho AI.

## Các ví dụ cấu hình

### Chỉ sử dụng tính năng cho m thanh và Video
```json5
{
  "tools": {
    "media": {
      "audio": { "enabled": true },
      "video": { "enabled": true },
      "image": { "enabled": false }
    }
  }
}
```

## Kiểm tra trạng thái
Khi tính năng này hoạt động, lệnh `/status` trong hộp chat sẽ hiển thị một dòng thông báo ngắn gọn:
`📎 Media: image ok (openai/gpt-4o) · audio skipped (maxBytes)`

---
Tài liệu liên quan: [Cấu hình Gateway](../../gateway/configuration.vi.md), [Hỗ trợ Hình ảnh & Đa phương tiện](./images.vi.md).
