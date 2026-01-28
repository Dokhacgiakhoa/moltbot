---
summary: "Tổng quan về dòng mô hình GLM và cách sử dụng trong Moltbot"
read_when:
  - Bạn muốn dùng các mô hình GLM thông qua nền tảng Z.AI
---
# Các mô hình GLM

GLM là một **dòng mô hình** AI mạnh mẽ (không phải tên công ty) được cung cấp thông qua nền tảng Z.AI. Trong Moltbot, các mô hình GLM được truy cập thông qua nhà cung cấp `zai`.

## Thiết lập qua CLI
```bash
moltbot onboard --auth-choice zai-api-key
```

## Ví dụ cấu hình
```json5
{
  env: { ZAI_API_KEY: "sk-..." },
  agents: { defaults: { model: { primary: "zai/glm-4.7" } } }
}
```

## Ghi chú
- Các phiên bản GLM phổ biến bao gồm `glm-4.7` và `glm-4.6`.
- Bạn có thể xem chi tiết về cách lấy mã khóa API tại trang tài liệu của Z.AI.

---
Tài liệu liên quan: [Nhà cung cấp Z.AI](./zai.vi.md).
