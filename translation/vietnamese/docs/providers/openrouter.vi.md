---
summary: "Sử dụng API hợp nhất của OpenRouter để truy cập hàng trăm mô hình AI trong Moltbot"
read_when:
  - Bạn muốn dùng một mã API key duy nhất cho nhiều loại chatbot khác nhau
---
# OpenRouter

OpenRouter cung cấp một **API hợp nhất** cho phép bạn truy cập vào hàng trăm mô hình AI (Claude, GPT, Gemini, Llama...) chỉ với một điểm kết nối và một mã API key duy nhất. Nó hoàn toàn tương thích với chuẩn của OpenAI.

## Thiết lập qua CLI
```bash
moltbot onboard --auth-choice apiKey --token-provider openrouter --token "$OPENROUTER_API_KEY"
```

## Ví dụ cấu hình
```json5
{
  env: { OPENROUTER_API_KEY: "sk-or-..." },
  agents: {
    defaults: {
      model: { primary: "openrouter/anthropic/claude-sonnet-4-5" }
    }
  }
}
```

## Các lưu ý
- Định dạng gọi model sẽ là: `openrouter/<nhà_cung_cấp>/<tên_model>`.
- OpenRouter rất hữu ích nếu bạn muốn thử nghiệm nhiều loại model khác nhau mà không muốn phải đăng ký tài khoản ở từng nơi.

---
Tài liệu liên quan: [Tất cả nhà cung cấp](./index.vi.md), [Lựa chọn mô hình](../../concepts/models.vi.md).
