---
summary: "Tài liệu tham khảo lệnh `moltbot skills` (Liệt kê/Thông tin/Kiểm tra) và điều kiện sử dụng kỹ năng"
read_when:
  - Bạn muốn xem những kỹ năng nào đang khả dụng và sẵn sàng hoạt động
  - Bạn muốn tìm lý do tại sao một kỹ năng không hoạt động (thiếu môi trường, thiếu cấu hình)
---

# `moltbot skills`

Kiểm tra các kỹ năng (kỹ năng đi kèm, kỹ năng trong không gian làm việc và các cài đặt đè). Lệnh này giúp bạn biết kỹ năng nào đủ điều kiện chạy và kỹ năng nào đang thiếu các yêu cầu cần thiết.

Tài liệu liên quan:
- Hệ thống kỹ năng: [Tổng quan về Kỹ năng](../../tools/skills.vi.md)
- Cấu hình kỹ năng: [Cấu hình chi tiết](../../tools/skills-config.md)
- Cài đặt từ ClawdHub: [ClawdHub](../../tools/clawdhub.md)

## Các lệnh chính

```bash
# Liệt kê tất cả các kỹ năng đã cài đặt
moltbot skills list

# Chỉ liệt kê các kỹ năng đủ điều kiện hoạt động
moltbot skills list --eligible

# Xem chi tiết yêu cầu của một kỹ năng cụ thể
moltbot skills info <tên-kỹ-năng>

# Kiểm tra nhanh xem hệ thống còn thiếu gì (binaries, môi trường...)
moltbot skills check
```

**Gợi ý**: Bạn nên sử dụng `npx clawdhub` để tìm kiếm, cài đặt và đồng bộ hóa các kỹ năng mới từ cộng đồng một cách dễ dàng nhất.
