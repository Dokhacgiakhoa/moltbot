---
summary: "Plugin Cuộc gọi thoại (Voice Call): Thực hiện cuộc gọi đi và nhận cuộc gọi đến qua Twilio/Telnyx/Plivo"
read_when:
  - Bạn muốn Bot có khả năng gọi điện thoại trực tiếp cho bạn hoặc người khác
---

# Gọi điện thoại (Plugin)

Moltbot hỗ trợ thực hiện các cuộc gọi điện thoại thông qua một plugin mở rộng. Bạn có thể dùng nó để gửi thông báo bằng giọng nói hoặc thực hiện các cuộc hội thoại đa lượt với AI.

Các nhà cung cấp hiện hỗ trợ:
- **Twilio**: Phổ biến nhất, hỗ trợ tốt nhất cho việc truyền hiệu ứng âm thanh.
- **Telnyx**: Lựa chọn thay thế với chi phí thấp.
- **Plivo**: Hỗ trợ tốt cho các cuộc gọi tự động bằng XML.

## Cài đặt nhanh
1. Cài đặt plugin từ npm:
   ```bash
   moltbot plugins install @moltbot/voice-call
   ```
2. Khởi động lại Gateway.
3. Cấu hình các thông tin API (như `accountSid`, `authToken`) trong tệp `moltbot.json`.

## Cấu hình mẫu (cho Twilio)
```json5
{
  "plugins": {
    "entries": {
      "voice-call": {
        "enabled": true,
        "config": {
          "provider": "twilio",
          "fromNumber": "+15550001234", // Số điện thoại của Bot
          "twilio": {
            "accountSid": "AC...",
            "authToken": "..."
          }
        }
      }
    }
  }
}
```

## Giọng nói cho cuộc gọi (TTS)
Plugin này sử dụng các cài đặt giọng nói chung của hệ thống (OpenAI hoặc ElevenLabs). Bạn có thể chỉnh sửa giọng nói riêng cho việc gọi điện nếu muốn trong phần cấu hình plugin.

## Sử dụng qua dòng lệnh (CLI)
Bạn có thể ra lệnh cho Bot gọi điện trực tiếp từ máy tính của mình:
```bash
moltbot voicecall call --to "+84901234567" --message "Chào bạn, đây là Moltbot đang gọi!"
```

## Tích hợp cho AI (Agent Tool)
AI có thể tự động gọi điện nếu bạn cấp quyền cho nó sử dụng công cụ `voice_call`. Các hành động AI có thể làm là:
- `initiate_call`: Bắt đầu một cuộc gọi mới.
- `speak_to_user`: Nói một câu với người đang nghe máy.
- `end_call`: Kết thúc cuộc gọi.

---
Tài liệu liên quan: [Cài đặt Plugin](./index.vi.md), [Quản lý giọng nói](../../nodes/talk.vi.md).
