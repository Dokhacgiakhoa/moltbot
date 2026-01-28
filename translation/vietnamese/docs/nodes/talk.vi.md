---
summary: "Chế độ Trò chuyện (Talk mode): Hội thoại bằng giọng nói liên tục sử dụng công nghệ ElevenLabs"
read_when:
  - Bạn muốn trò chuyện trực tiếp bằng giọng nói với Bot trên điện thoại hoặc máy tính
---

# Chế độ Trò chuyện (Talk Mode)

Chế độ Trò chuyện là một vòng lặp hội thoại bằng giọng nói liên tục:
1. Bot lắng nghe lời nói của bạn.
2. Chuyển lời nói thành văn bản và gửi cho mô hình AI.
3. Chờ đợi câu trả lời từ AI.
4. Phát câu trả lời đó bằng giọng nói thông qua ElevenLabs.

## Hành vi trên macOS
- Hiển thị một **lớp giao diện phủ (overlay)** trên màn hình khi chế độ này được bật.
- Các trạng thái: **Đang nghe (Listening)** → **Đang suy nghĩ (Thinking)** → **Đang nói (Speaking)**.
- **Tự động ngắt lời**: Nếu bạn bắt đầu nói trong khi Bot đang trả lời, Bot sẽ tự động dừng phát âm thanh và chuẩn bị lắng nghe lượt tiếp theo của bạn.

## Điều khiển giọng nói trong câu trả lời
Bot có thể thay đổi giọng nói của mình ngay trong lúc chat bằng cách thêm một dòng lệnh JSON vào đầu câu trả lời:
`{"voice":"id-giọng-nói","once":true}`

- `once: true`: Chỉ áp dụng cho câu trả lời này.
- Nếu không có `once`, giọng nói này sẽ trở thành giọng nói mặc định mới của Bot.

## Cấu hình (`moltbot.json`)
```json5
{
  "talk": {
    "voiceId": "id_giọng_nói_eleven_labs",
    "apiKey": "khóa_api_eleven_labs",
    "interruptOnSpeech": true // Tự động dừng khi người dùng nói chen vào
  }
}
```

## Giao diện trên macOS
Bạn có thể thấy các hiệu ứng đặc biệt trên màn hình:
- **Đang nghe**: Đám mây nhấp nháy theo âm lượng mic.
- **Đang suy nghĩ**: Hiệu ứng chuyển động chìm xuống.
- **Đang nói**: Các vòng tròn lan tỏa.
- Nhấp vào đám mây để dừng Bot đang nói.
- Nhấp vào dấu X để thoát chế độ trò chuyện.

## Lưu ý
- Yêu cầu quyền truy cập **Microphone** và **Nhận dạng giọng nói (Speech Recognition)**.
- Sử dụng API của ElevenLabs để có giọng nói tự nhiên nhất với độ trễ thấp.

---
Tài liệu liên quan: [Đánh thức bằng giọng nói](./voicewake.vi.md), [Ứng dụng macOS](../platforms/macos.vi.md).
