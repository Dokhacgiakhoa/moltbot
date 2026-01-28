---
summary: "Gọi trực tiếp một công cụ (tool) thông qua cổng HTTP của Gateway"
read_when:
  - Bạn muốn tích hợp Moltbot vào các đoạn mã tự động hóa của bạn mà không cần chạy toàn bộ Agent
---

# Gọi công cụ trực tiếp (HTTP)

Gateway cung cấp một địa chỉ HTTP đơn giản để bạn có thể gọi thực thi một công cụ bất kỳ mà không cần phải thông qua giao diện chat của Agent.

- **Địa chỉ**: `POST /tools/invoke`
- **Cổng**: Cùng cổng với Gateway.

## Xác thực
Sử dụng mã xác thực Gateway của bạn gửi kèm trong tiêu đề:
`Authorization: Bearer <ma-token-cua-ban>`

## Cấu trúc yêu cầu (Body)
```json
{
  "tool": "sessions_list",
  "action": "json",
  "args": {},
  "sessionKey": "main"
}
```
- **`tool`**: Tên công cụ muốn gọi (ví dụ: `exec`, `read`, `sessions_list`).
- **`args`**: Các tham số đầu vào cho công cụ đó.
- **`sessionKey`**: (Tùy chọn) Chạy công cụ này trong phiên làm việc nào.

## Kiểm soát quyền hạn
Mọi yêu cầu gửi đến đây đều đi qua **Dây chuyền kiểm soát chính sách (Policy chain)** giống hệt như khi Agent chạy. Nếu một công cụ bị cấm trong cấu hình `moltbot.json`, bạn cũng sẽ không thể gọi nó qua API này (hệ thống sẽ trả về lỗi 404).

## Ví dụ thực tế (Dùng curl)
```bash
curl -sS http://127.0.0.1:18789/tools/invoke \
  -H 'Authorization: Bearer MA_TOKEN_CUA_BAN' \
  -H 'Content-Type: application/json' \
  -d '{
    "tool": "sessions_list",
    "args": {}
  }'
```

---
Tài liệu liên quan: [Danh sách công cụ](../../tools/index.vi.md), [Cấu hình hệ thống](./configuration.vi.md).
