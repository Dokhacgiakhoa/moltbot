---
summary: "Cổng HTTP /v1/responses tương thích với chuẩn OpenResponses từ Gateway"
read_when:
  - Bạn đang xây dựng các công cụ cao cấp cần gửi hình ảnh, tệp tin hoặc gọi hàm API từ phía ứng dụng khách
---

# API OpenResponses (HTTP)

Moltbot hỗ trợ chuẩn OpenResponses thông qua địa chỉ `POST /v1/responses`. Tính năng này mạnh mẽ hơn chuẩn OpenAI thông thường vì nó cho phép gửi kèm hình ảnh, tệp tin và quản lý các lượt gọi công cụ (tools) một cách linh hoạt.

## Các đặc điểm nổi bật
- **Đầu vào dựa trên mục (Items)**: Bạn có thể gửi một mảng các mục bao gồm văn bản, hình ảnh (`input_image`) và tệp tin (`input_file`).
- **Hỗ trợ tệp tin và mã nguồn**: Agent có thể đọc nội dung tệp (văn bản, PDF, mã nguồn) được gửi trực tiếp qua API.
- **Công cụ phía client (Function tools)**: Bạn có thể định nghĩa các công cụ mà AI có thể yêu cầu ứng dụng của bạn thực thi.

## Cách bật tính năng
Thay đổi cấu hình trong `moltbot.json`:
```json5
{
  "gateway": {
    "http": {
      "endpoints": {
        "responses": { "enabled": true }
      }
    }
  }
}
```

## Chế độ gửi tệp tin
- **Hình ảnh**: Hỗ trợ JPEG, PNG, GIF, WebP (Tối đa 10MB). Có thể gửi qua đường dẫn URL hoặc dữ liệu dạng Base64.
- **Tài liệu**: Hỗ trợ PDF (tự động trích xuất văn bản), Markdown, HTML, JSON, CSV (Tối đa 5MB). Nội dung tệp sẽ được nạp trực tiếp vào ngữ cảnh của AI nhưng không lưu lại vĩnh viễn trong lịch sử chat để tiết kiệm bộ nhớ.

---
Tài liệu liên quan: [API tương thích OpenAI](./openai-http-api.vi.md), [Cấu hình tệp tin](../concepts/context.vi.md).
