---
summary: "Tài liệu tham khảo lệnh `moltbot voicecall` (Các lệnh cho plugin cuộc gọi thoại)"
read_when:
  - Bạn sử dụng plugin voice-call và muốn thực hiện cuộc gọi qua dòng lệnh
---

# `moltbot voicecall`

`voicecall` là bộ lệnh được cung cấp bởi một plugin. Lệnh này chỉ xuất hiện nếu bạn đã cài đặt và kích hoạt plugin cuộc gọi thoại (voice-call).

Tài liệu liên quan:
- Plugin Cuộc gọi thoại: [Voice Call](../../plugins/voice-call.md)

## Các lệnh phổ biến

```bash
# Kiểm tra trạng thái của một cuộc gọi đang diễn ra
moltbot voicecall status --call-id <id>

# Thực hiện cuộc gọi thông báo tự động
moltbot voicecall call --to "+8490xxxxxxx" --message "Chào chủ nhân, hệ thống đã hoàn tất sao lưu" --mode notify

# Tiếp tục cuộc trò chuyện trong cuộc gọi
moltbot voicecall continue --call-id <id> --message "Bạn có câu hỏi nào nữa không?"

# Kết thúc cuộc gọi
moltbot voicecall end --call-id <id>
```

## Công khai Webhook (Tailscale)
Dùng để cho phép các dịch vụ điện thoại bên thứ ba (như Twilio) có thể gửi tín hiệu về máy của bạn:
```bash
moltbot voicecall expose --mode serve
moltbot voicecall unexpose
```

Lưu ý bảo mật: Chỉ công khai các điểm cuối webhook trong các mạng mà bạn thực sự tin tưởng.
