---
summary: "Thiết lập Brave Search API cho tính năng tìm kiếm web (web_search)"
---

# Brave Search API

Moltbot sử dụng Brave Search làm nhà cung cấp mặc định cho tính năng `web_search` (tìm kiếm web).

## Nhận mã API key

1.  Tạo tài khoản Brave Search API tại: https://brave.com/search/api/
2.  Trong bảng điều khiển, chọn gói **Data for Search** và tạo một mã API key.
3.  Lưu mã này vào cấu hình (khuyên dùng) hoặc đặt biến môi trường `BRAVE_API_KEY` cho Gateway.

## Ví dụ cấu hình

```json
{
  "tools": {
    "web": {
      "search": {
        "provider": "brave",
        "apiKey": "MÃ_API_KEY_CỦA_BẠN",
        "maxResults": 5,
        "timeoutSeconds": 30
      }
    }
  }
}
```

## Lưu ý

- Gói "Data for AI" **không** tương thích với tính năng `web_search`.
- Brave có cung cấp gói miễn phí cũng như các gói trả phí; hãy kiểm tra cổng thông tin Brave API để biết giới hạn sử dụng hiện tại.

---
Tài liệu liên quan: [Công cụ Web](../tools/web.vi.md), [Tìm kiếm Web](../tools/web_search.vi.md).
