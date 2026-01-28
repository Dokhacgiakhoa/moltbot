---
summary: "Viết các công cụ (tools) cho Agent trong một plugin (định nghĩa schema, các công cụ tùy chọn, danh sách cho phép)"
read_when:
  - Bạn muốn thêm một công cụ mới cho Agent thông qua một plugin
---

# Công cụ Agent trong Plugin

Các plugin của Moltbot có thể đăng ký các **công cụ dành cho Agent** (dưới dạng hàm JSON-schema). Các công cụ này sẽ được cung cấp cho mô hình AI (LLM) sử dụng trong quá trình hội thoại. Bạn có thể thiết lập công cụ là **bắt buộc** (luôn sẵn sàng) hoặc **tùy chọn** (phải bật thủ công).

## Cách đăng ký công cụ cơ bản

```ts
import { Type } from "@sinclair/typebox";

export default function (api) {
  api.registerTool({
    name: "ten_cong_cu_cua_toi",
    description: "Mô tả công cụ làm gì đó",
    parameters: Type.Object({
      input: Type.String(),
    }),
    async execute(_id, params) {
      // Thực hiện logic tại đây
      return { content: [{ type: "text", text: params.input }] };
    },
  });
}
```

## Công cụ tùy chọn (Opt-in)

Các công cụ tùy chọn sẽ **không bao giờ** tự động được bật. Người dùng phải thêm chúng vào danh sách cho phép (`allowlist`) của từng Agent.

```ts
api.registerTool(
  {
    name: "cong_cu_quy_trinh",
    // ... các thông số khác
  },
  { optional: true }, // Đánh dấu là công cụ tùy chọn
);
```

Để bật công cụ này, bạn cấu hình trong `moltbot.json`:

```json5
{
  "agents": {
    "list": [
      {
        "id": "main",
        "tools": {
          "allow": ["cong_cu_quy_trinh"] // Thêm tên công cụ vào đây
        }
      }
    ]
  }
}
```

## Các quy tắc và mẹo
- Tên công cụ không được trùng với các công cụ cốt lõi của hệ thống.
- Nên đặt công cụ ở chế độ `optional: true` nếu công cụ đó có thể gây ra các tác động bên ngoài hoặc yêu cầu các khóa bảo mật riêng.

---
Tài liệu liên quan: [Hệ thống công cụ](../../tools/index.vi.md), [Viết Plugin](./writing-plugins.vi.md).
