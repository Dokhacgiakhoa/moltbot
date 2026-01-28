---
summary: "Các tác vụ LLM chỉ dùng JSON cho các quy trình làm việc (công cụ mở rộng tùy chọn)"
read_when:
  - Bạn muốn một bước xử lý của AI chỉ trả về dữ liệu cấu trúc JSON
  - Cần xác thực dữ liệu đầu ra để tự động hóa quy trình
---
# Tác vụ LLM (`llm-task`)

`llm-task` là một **công cụ mở rộng (plugin)** giúp thực hiện các nhiệm vụ AI với đầu ra thuần túy là định dạng JSON. Bạn có thể yêu cầu AI xác thực kết quả này theo một cấu trúc (JSON Schema) định sẵn để đảm bảo máy tính luôn đọc được.

Công cụ này cực kỳ hữu ích cho các hệ thống tự động hóa như **Lobster**, nơi bạn cần một bước ra quyết định của AI nhưng không muốn nó nói thêm bất kỳ câu xả giao nào.

## Ví dụ thực tế
Bạn có thể dùng công cụ này để phân loại email:
- **Đầu vào**: "Tôi muốn đặt hàng một chiếc máy tính."
- **Nhiệm vụ AI**: "Xác định mục đích của khách hàng."
- **Kết quả JSON**: `{"muc_dich": "mua_hang", "san_pham": "may_tinh"}`

## Đặc điểm nổi bật
- **Chỉ xuất JSON**: AI được hướng dẫn nghiêm ngặt để không bao giờ in thêm văn bản thừa hay các dấu mã nguồn (` ``` `).
- **Xác thực dữ liệu**: Nếu bạn cung cấp một bộ khung (schema), công cụ sẽ chỉ chấp nhận kết quả nếu AI làm đúng theo khung đó.
- **An toàn**: Trong lượt chạy này, AI không được tiếp cận với bất kỳ công cụ hệ thống nào khác, đảm bảo nó chỉ xử lý dữ liệu mà không gây ra tác động phụ.

---
Tài liệu liên quan: [Cơ chế Pipeline Lobster](./lobster.vi.md), [Plugin](../../plugin.vi.md).
