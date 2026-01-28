---
summary: "Sử dụng OpenCode Zen (Danh sách mô hình chọn lọc) cho lập trình trong Moltbot"
read_when:
  - Bạn muốn sử dụng các mô hình đã được đội ngũ OpenCode tối ưu cho việc viết mã
---
# OpenCode Zen

OpenCode Zen là một **danh sách các mô hình AI được tuyển chọn** và khuyên dùng bởi đội ngũ OpenCode dành cho các trợ lý lập trình. Đây là một dịch vụ lưu trữ mô hình (hosted) giúp bạn truy cập nhanh vào các model mạnh nhất thông qua một mã API key duy nhất. Hiện Zen đang trong giai đoạn thử nghiệm (beta).

## Thiết lập qua CLI
```bash
moltbot onboard --auth-choice opencode-zen
```

## Ví dụ cấu hình
```json5
{
  env: { OPENCODE_API_KEY: "sk-..." },
  agents: { defaults: { model: { primary: "opencode/claude-opus-4-5" } } }
}
```

## Lưu ý
- OpenCode Zen tính phí dựa trên số lượng yêu cầu (billing per request). Bạn có thể kiểm tra chi tiết bảng giá và lịch sử sử dụng tại bảng điều khiển của OpenCode.
- Các mô hình trong danh sách của Zen luôn được cập nhật để đảm bảo khả năng lập trình tốt nhất.

---
Tài liệu liên quan: [Danh sách nhà cung cấp](./index.vi.md), [Lựa chọn mô hình](../../concepts/models.vi.md).
