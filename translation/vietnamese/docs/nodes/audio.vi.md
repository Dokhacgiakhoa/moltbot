---
summary: "Cách các tệp âm thanh/tin nhắn thoại được tải về, chuyển thành văn bản và đưa vào câu trả lời của Bot"
read_when:
  - Bạn muốn thay đổi cách Bot xử lý tin nhắn thoại hoặc chuyển âm thanh thành văn bản
---

# m thanh / Tin nhắn thoại

## Cách hoạt động
- **Hiểu phương tiện truyền thông (m thanh)**: Nếu tính năng này được bật, Moltbot sẽ:
  1. Tìm tệp âm thanh đính kèm và tải về nếu cần.
  2. Kiểm tra dung lượng tệp so với giới hạn `maxBytes`.
  3. Sử dụng mô hình AI hoặc công cụ dòng lệnh (CLI) để chuyển âm thanh thành văn bản (transcription).
  4. Nếu thành công, Bot sẽ chèn văn bản này vào nội dung hội thoại với nhãn `[Audio]` và biến `{{Transcript}}`.
- **Phân tích lệnh**: Sau khi chuyển thành văn bản, Bot có thể hiểu các lệnh (ví dụ như lệnh bắt đầu bằng `/`) có trong tin nhắn thoại đó.

## Tự động phát hiện (Mặc định)
Nếu bạn không cấu hình cụ thể, Moltbot sẽ tự động tìm các công cụ chuyển âm thanh theo thứ tự:
1. **Các công cụ cài đặt tại máy (CLI)**: `whisper`, `whisper-cli`, `sherpa-onnx-offline`.
2. **Gemini CLI**: Sử dụng mô hình Google Gemini.
3. **Các khóa API của nhà cung cấp**: Ưu tiên OpenAI → Groq → Deepgram → Google.

Để tắt tính năng này, hãy đặt cấu hình `tools.media.audio.enabled: false`.

## Ví dụ cấu hình

### Kết hợp API OpenAI và công cụ Whisper tại máy
```json5
{
  tools: {
    media: {
      audio: {
        enabled: true,
        models: [
          { provider: "openai", model: "gpt-4o-mini-transcribe" },
          {
            type: "cli",
            command: "whisper",
            args: ["--model", "base", "{{MediaPath}}"]
          }
        ]
      }
    }
  }
}
```

## Các lưu ý và giới hạn
- Giới hạn dung lượng mặc định là 20MB. Tệp lớn hơn sẽ bị bỏ qua.
- Văn bản chuyển đổi được cung cấp cho các mẫu tin nhắn qua biến `{{Transcript}}`.
- Bạn có thể chuyển đổi nhiều tin nhắn thoại cùng lúc bằng cách bật `tools.media.audio.attachments`.

---
Tài liệu liên quan: [Hiểu phương tiện truyền thông](./media-understanding.vi.md), [Nhà cung cấp Deepgram](../providers/deepgram.vi.md).
