---
summary: "Cổng HTTP /v1/chat/completions tương thích với OpenAI từ Gateway"
read_when:
  - Bạn muốn dùng các ứng dụng hoặc công cụ vốn được thiết kế cho OpenAI để kết nối với Moltbot
---

# API tương thích OpenAI (HTTP)

Gateway của Moltbot cung cấp một cổng (endpoint) nhỏ tương thích với chuẩn OpenAI Chat Completions. Tính năng này **bị tắt theo mặc định**. Để sử dụng, bạn cần bật nó trong tệp cấu hình.

- **Địa chỉ**: `POST /v1/chat/completions`
- **Cổng**: Cùng cổng với Gateway (Ví dụ: `http://localhost:18789/v1/chat/completions`).

Về bản chất, các yêu cầu gửi đến đây sẽ được thực thi như một lượt chạy Agent bình thường trong Moltbot.

## Xác thực
Sử dụng mã xác thực Gateway của bạn. Gửi mã này trong tiêu đề (header) của yêu cầu:
`Authorization: Bearer <token_cua_ban>`

## Chọn Agent
Bạn không cần thêm tiêu đề tùy chỉnh, chỉ cần ghi ID của Agent vào trường `model` trong yêu cầu OpenAI:
- `model: "moltbot:main"` (Dùng Agent tên 'main')
- `model: "agent:beta"` (Dùng Agent tên 'beta')

## Bật tính năng này
Thêm đoạn sau vào tệp cấu hình `moltbot.json`:
```json5
{
  "gateway": {
    "http": {
      "endpoints": {
        "chatCompletions": { "enabled": true }
      }
    }
  }
}
```

## Luồng dữ liệu (Streaming)
Hỗ trợ đầy đủ chế độ `stream: true` để nhận kết quả ngay khi AI vừa tạo ra từng chữ (Server-Sent Events).

---
Tài liệu liên quan: [Cấu hình hệ thống](./configuration.vi.md), [Nhà cung cấp AI](../concepts/model-providers.vi.md).
