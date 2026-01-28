---
summary: "Tính năng chuyển văn bản thành giọng nói (TTS) cho các phản hồi từ Bot"
---

# Chuyển văn bản thành giọng nói (TTS)

Moltbot có thể chuyển đổi các câu trả lời văn bản thành âm thanh bằng cách sử dụng ElevenLabs, OpenAI hoặc Edge TTS. Tính năng này hoạt động trên mọi kênh hỗ trợ gửi âm thanh; riêng Telegram sẽ nhận được dưới dạng tin nhắn thoại (voice-note) hình tròn.

## Các dịch vụ hỗ trợ

- **ElevenLabs**: Nhà cung cấp chính hoặc dự phòng.
- **OpenAI**: Nhà cung cấp chính hoặc dự phòng; cũng được dùng để tóm tắt văn bản dài.
- **Edge TTS**: Nhà cung cấp mặc định khi không có API key (sử dụng dịch vụ của Microsoft Edge, không tốn phí).

## Thiết lập

Bản thân tính năng TTS mặc định là **Tắt**. Bạn có thể bật nó trong cấu hình bằng biến `messages.tts.auto` hoặc bật theo từng phiên trò chuyện bằng lệnh `/tts always` (hoặc `/tts on`).

### Ví dụ cấu hình tối giản (Dùng Edge TTS miễn phí)

```json
{
  "messages": {
    "tts": {
      "auto": "always",
      "provider": "edge"
    }
  }
}
```

### Cấu hình nâng cao (OpenAI làm chính, ElevenLabs dự phòng)

```json
{
  "messages": {
    "tts": {
      "auto": "always",
      "provider": "openai",
      "openai": {
        "apiKey": "MÃ_OPENAI_KEY",
        "voice": "alloy"
      },
      "elevenlabs": {
        "apiKey": "MÃ_ELEVENLABS_KEY",
        "voiceId": "ID_GIỌNG_NÓI"
      }
    }
  }
}
```

## Các chế độ tự động (`auto`)

- `off`: Tắt hoàn toàn.
- `always`: Luôn phát âm thanh cho mọi câu trả lời.
- `inbound`: Chỉ phát âm thanh khi người dùng gửi tin nhắn thoại trước.
- `tagged`: Chỉ phát âm thanh khi câu trả lời có chứa nhãn `[[tts]]`.

## Cơ chế hoạt động

Khi được bật, Moltbot sẽ:
- Bỏ qua TTS nếu câu trả lời đã có sẵn file đa phương tiện (ảnh/video).
- Bỏ qua các câu trả lời quá ngắn (< 10 ký tự).
- Tự động tóm tắt các câu trả lời quá dài (để tiết kiệm chi phí Token) trước khi chuyển thành giọng nói.
- Đính kèm file âm thanh được tạo vào câu trả lời gửi cho bạn.

## Các lệnh điều khiển nhanh

Bạn có thể gõ trực tiếp trong chat:
- `/tts off`: Tắt TTS cho phiên này.
- `/tts always`: Luôn bật TTS.
- `/tts status`: Kiểm tra trạng thái và nhà cung cấp hiện tại.
- `/tts provider openai`: Đổi nhà cung cấp sang OpenAI.
- `/tts audio [nội dung]`: Chỉ tạo âm thanh cho một tin nhắn duy nhất này.

---
Tài liệu liên quan: [Cấu hình Gateway](../../gateway/configuration.vi.md), [Các lệnh dòng lệnh](../tools/slash-commands.vi.md).
