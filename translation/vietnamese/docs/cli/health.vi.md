---
summary: "Tài liệu tham khảo lệnh `moltbot health` (Kiểm tra điểm cuối sức khỏe Gateway qua RPC)"
read_when:
  - Bạn muốn kiểm tra nhanh xem Gateway có đang hoạt động tốt hay không
---

# `moltbot health`

Lấy thông tin sức khỏe từ Gateway đang chạy.

## Ví dụ sử dụng

```bash
# Kiểm tra nhanh
moltbot health

# Xuất kết quả dưới dạng JSON để sử dụng trong script
moltbot health --json

# Hiển thị chi tiết (Running probes)
moltbot health --verbose
```

## Các lưu ý:
- Chế độ `--verbose` sẽ thực hiện các lượt thăm dò thực tế và hiển thị thời gian phản hồi của từng tài khoản cấu hình.
- Nếu bạn có nhiều Agent, kết quả sẽ bao gồm cả tình trạng lưu trữ phiên trò chuyện của từng Agent đó.

---
Tài liệu liên quan: [Chẩn đoán hệ thống](./status.vi.md), [Hướng dẫn Onboarding](../../start/onboarding.vi.md).
