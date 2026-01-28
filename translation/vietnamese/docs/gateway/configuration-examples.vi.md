---
summary: "Các ví dụ cấu hình chuẩn cho các thiết lập Moltbot phổ biến"
read_when:
  - Bạn mới bắt đầu cấu hình Moltbot lần đầu
  - Bạn đang tìm kiếm các mẫu cấu hình cho các nhu cầu cụ thể
---

# Các ví dụ cấu hình

Các ví dụ dưới đây tuân thủ đúng cấu trúc (schema) hiện tại của Moltbot. Để xem tài liệu chi tiết cho từng trường, vui lòng xem mục [Cấu hình](./configuration.vi.md).

## Bắt đầu nhanh

### Cấu hình tối giản
```json5
{
  "agent": { "workspace": "~/clawd" },
  "channels": { "whatsapp": { "allowFrom": ["+84901234567"] } }
}
```
Lưu vào tệp `~/.clawdbot/moltbot.json` và bạn có thể nhắn tin cho Bot từ số điện thoại đó.

### Cấu hình khuyên dùng cho người mới
```json5
{
  "identity": {
    "name": "Moltbot",
    "theme": "trợ lý đắc lực",
    "emoji": "🦞"
  },
  "agent": {
    "workspace": "~/clawd",
    "model": { "primary": "anthropic/claude-3-5-sonnet" }
  },
  "channels": {
    "whatsapp": {
      "allowFrom": ["+84901234567"],
      "groups": { "*": { "requireMention": true } }
    }
  }
}
```

## Các mô hình phổ biến

### Bot cho công việc (Hạn chế quyền truy cập)
```json5
{
  "identity": {
    "name": "WorkBot",
    "theme": "trợ lý chuyên nghiệp"
  },
  "agent": {
    "workspace": "~/work-clawd",
    "elevated": { "enabled": false } // Tắt quyền thực thi trên máy chủ
  },
  "channels": {
    "slack": {
      "enabled": true,
      "botToken": "xoxb-...",
      "channels": {
        "#engineering": { "allow": true, "requireMention": true },
        "#general": { "allow": true, "requireMention": true }
      }
    }
  }
}
```

### Chỉ sử dụng các mô hình AI chạy cục bộ
```json5
{
  "agent": {
    "workspace": "~/clawd",
    "model": { "primary": "lmstudio/minimax-m2.1" }
  },
  "models": {
    "mode": "merge",
    "providers": {
      "lmstudio": {
        "baseUrl": "http://127.0.0.1:1234/v1",
        "apiKey": "lmstudio",
        "api": "openai-responses",
        "models": [
          {
            "id": "minimax-m2.1",
            "name": "MiniMax M2.1",
            "reasoning": false,
            "contextWindow": 196608
          }
        ]
      }
    }
  }
}
```

## Mẹo nhỏ
- Nếu bạn để `dmPolicy: "open"`, danh sách `allowFrom` phải chứa ký tự `"*"` để cho phép tất cả mọi người.
- Định danh người dùng (ID) khác nhau tùy theo nền tảng (số điện thoại cho WhatsApp, ID số cho Telegram). Hãy kiểm tra tài liệu của từng kênh để lấy đúng định dạng.
- Bạn có thể thêm các phần như `web`, `browser`, `discovery` sau này khi đã quen với cấu hình cơ bản.

---
Tài liệu liên quan: [Cấu hình chi tiết](./configuration.vi.md), [Xử lý lỗi](./troubleshooting.vi.md).
