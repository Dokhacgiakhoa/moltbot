---
summary: "Thiết lập Perplexity Sonar cho tính năng tìm kiếm web (web_search)"
---

# Perplexity Sonar

Moltbot có thể sử dụng Perplexity Sonar cho công cụ `web_search`. Bạn có thể kết nối trực tiếp qua API của Perplexity hoặc thông qua OpenRouter.

## Các tùy chọn API

### Kết nối trực tiếp Perplexity
- **Base URL**: `https://api.perplexity.ai`
- **Biến môi trường**: `PERPLEXITY_API_KEY`

### Qua OpenRouter (Thay thế)
- **Base URL**: `https://openrouter.ai/api/v1`
- **Biến môi trường**: `OPENROUTER_API_KEY`
- Hỗ trợ thanh toán trước hoặc bằng tiền điện tử.

## Ví dụ cấu hình

```json
{
  "tools": {
    "web": {
      "search": {
        "provider": "perplexity",
        "perplexity": {
          "apiKey": "pplx-...",
          "baseUrl": "https://api.perplexity.ai",
          "model": "perplexity/sonar-pro"
        }
      }
    }
  }
}
```

## Cách Moltbot chọn nhà cung cấp

Nếu bạn không đặt `baseUrl`, Moltbot sẽ tự chọn dựa trên định dạng API key:
- `PERPLEXITY_API_KEY` hoặc mã bắt đầu bằng `pplx-...` → Dùng trực tiếp Perplexity.
- `OPENROUTER_API_KEY` hoặc mã bắt đầu bằng `sk-or-...` → Dùng OpenRouter.

## Các mô hình hỗ trợ
- `perplexity/sonar`: Giải đáp thắc mắc nhanh kèm tìm kiếm web.
- `perplexity/sonar-pro` (mặc định): Suy luận đa bước kèm tìm kiếm web.
- `perplexity/sonar-reasoning-pro`: Nghiên cứu chuyên sâu.

---
Tài liệu liên quan: [Công cụ Web](../tools/web.vi.md), [Tìm kiếm Web](../tools/web_search.vi.md).
