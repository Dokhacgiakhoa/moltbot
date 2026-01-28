---
summary: "Sử dụng nền tảng Z.AI (các mô hình GLM) với Moltbot"
read_when:
  - Bạn muốn dùng mô hình GLM thông qua API của Z.AI
---
# Z.AI

Z.AI là nền tảng API cho các mô hình **GLM**. Nó cung cấp các chuẩn giao tiếp REST và sử dụng API key để xác thực. Bạn có thể tạo mã khóa này tại bảng điều khiển của Z.AI. 

## Thiết lập nhanh qua CLI
```bash
moltbot onboard --auth-choice zai-api-key
# Hoặc truyền trực tiếp nếu muốn thiết lập nhanh
moltbot onboard --zai-api-key "$ZAI_API_KEY"
```

## Ví dụ cấu hình
```json5
{
  env: { ZAI_API_KEY: "sk-..." },
  agents: { defaults: { model: { primary: "zai/glm-4.7" } } }
}
```

## Ghi chú
- Các mô hình GLM được gọi theo định dạng `zai/<tên_model>` (Ví dụ: `zai/glm-4.7`).
- Xem thêm phần [Tổng quan về dòng mô hình GLM](./glm.vi.md) để biết các phiên bản khả dụng.

---
Tài liệu liên quan: [Cấu hình Gateway](../gateway/configuration.vi.md), [Lựa chọn mô hình](../../concepts/models.vi.md).
