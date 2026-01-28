---
summary: "Tổng quan về các nhà cung cấp mô hình AI kèm ví dụ cấu hình và lệnh CLI"
read_when:
  - Bạn cần tham khảo cách thiết lập từng nhà cung cấp mô hình cụ thể
---

# Nhà cung cấp mô hình (Providers)

Trang này đề cập đến các **nhà cung cấp mô hình ngôn ngữ (LLM Providers)** (không phải các kênh chat như WhatsApp/Telegram).

## Các quy tắc nhanh

- Tên mô hình sử dụng định dạng `nhà-cung-cấp/tên-mô hình` (ví dụ: `openai/gpt-4o`).
- Bạn có thể dùng lệnh `moltbot onboard` để bắt đầu quá trình thiết lập tự động.

## Các nhà cung cấp hỗ trợ sẵn

Moltbot tích hợp sẵn danh mục các mô hình phổ biến nhất. Bạn chỉ cần nạp thông tin xác thực (Key hoặc OAuth) là có thể sử dụng ngay.

- **OpenAI**: Dùng biến môi trường `OPENAI_API_KEY`.
- **Anthropic (Claude)**: Hỗ trợ cả Khóa API truyền thống và Token đăng nhập.
- **Google Gemini**: Hỗ trợ qua API Key (`GEMINI_API_KEY`) hoặc đăng nhập OAuth qua Google Cloud/Antigravity.
- **OpenRouter**: Một cổng trung gian cho phép truy cập hàng trăm mô hình khác nhau từ nhiều nhà cung cấp.

## Nhà cung cấp thông qua cấu hình tùy chỉnh

Nếu bạn muốn sử dụng các máy chủ riêng hoặc các dịch vụ tương thích với OpenAI (như vLLM, Ollama), bạn có thể cấu hình chúng trong phần `models.providers`.

### Ollama (Mô hình chạy cục bộ)
Ollama là trình thực thi mô hình AI chạy ngay trên máy tính của bạn. Moltbot sẽ tự động phát hiện nếu Ollama đang chạy tại cổng mặc định `11434`.

```json
{
  "agents": {
    "defaults": {
      "model": { "primary": "ollama/llama3" }
    }
  }
}
```

---
Tài liệu liên quan: [Quản lý mô hình](./models.vi.md), [Cấu hình Gateway](../../gateway/configuration.vi.md).
