---
summary: "Tài liệu tham khảo lệnh `moltbot logs` (Theo dõi nhật ký Gateway qua RPC)"
read_when:
  - Bạn muốn xem nhật ký hoạt động của Gateway từ xa (không cần SSH)
  - Bạn cần thu thập dữ liệu nhật ký dưới dạng JSON cho các công cụ khác
---

# `moltbot logs`

Theo dõi nhật ký (logs) của Gateway thông qua giao thức RPC (hoạt động tốt ngay cả khi đang ở chế độ điều khiển từ xa).

Tài liệu liên quan:
- Tổng quan về Nhật ký: [Logging](../gateway/logging.vi.md)

## Ví dụ sử dụng

```bash
# Xem nhật ký hiện tại
moltbot logs

# Theo dõi nhật ký theo thời gian thực (real-time stream)
moltbot logs --follow

# Xuất nhật ký dưới định dạng JSON (mỗi dòng là một đối tượng JSON)
moltbot logs --json

# Giới hạn số dòng hiển thị gần nhất
moltbot logs --limit 500
```
