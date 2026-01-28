---
summary: "Danh sách và ví dụ thiết lập các nhà cung cấp mô hình AI"
read_when:
  - Bạn muốn xem nhanh các ví dụ về cài đặt AI cho Moltbot
---
# Các nhà cung cấp mô hình AI

Moltbot có thể sử dụng rất nhiều bộ não AI khác nhau. Hãy chọn một cái, xác thực và bắt đầu trò chuyện.

## Khởi động nhanh (Chỉ 2 bước)

1. **Xác thực**: Chạy lệnh `moltbot onboard` để khai báo API key của bạn.
2. **Chọn mô hình**: Thiết lập trong file `moltbot.json`:
   ```json5
   {
     agents: { defaults: { model: { primary: "anthropic/claude-opus-4-5" } } }
   }
   ```

## Các nhà cung cấp được hỗ trợ

| Nhà cung cấp | Đặc điểm | Tài liệu |
|---|---|---|
| **OpenAI** | Phổ biến nhất (GPT-4o) | [Xem hướng dẫn](./openai.vi.md) |
| **Anthropic** | Thông minh nhất (Claude 3.5) | [Xem hướng dẫn](./anthropic.vi.md) |
| **OpenRouter** | Nhiều model nhất | [Xem hướng dẫn](./openrouter.vi.md) |
| **Ollama** | AI cục bộ, miễn phí | [Xem hướng dẫn](./ollama.vi.md) |
| **Venice AI** | Ưu tiên quyền riêng tư | [Xem hướng dẫn](./venice.vi.md) |

Để xem toàn bộ danh mục hàng trăm mô hình khác (xAI, Groq, Mistral...), hãy tham khảo phần [Cấu hình nâng cao](../../concepts/model-providers.vi.md).

---
Tài liệu liên quan: [Giải thích về Model](../../concepts/models.vi.md), [Cấu hình Gateway](../gateway/configuration.vi.md).
