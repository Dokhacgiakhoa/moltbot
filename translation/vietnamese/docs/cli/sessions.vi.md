---
summary: "Tài liệu tham khảo lệnh `moltbot sessions` (Liệt kê các phiên trò chuyện đã lưu)"
read_when:
  - Bạn muốn xem danh sách các cuộc trò chuyện gần đây và dung lượng bộ nhớ chúng chiếm dụng
---

# `moltbot sessions`

Liệt kê các phiên trò chuyện (conversation sessions) đang được lưu trữ trong hệ thống.

## Ví dụ sử dụng

```bash
# Xem danh sách tất cả các phiên trò chuyện
moltbot sessions

# Xem các phiên trò chuyện có hoạt động trong vòng 120 phút qua
moltbot sessions --active 120

# Xuất kết quả dưới dạng JSON (dùng cho lập trình hoặc báo cáo)
moltbot sessions --json
```

---
Tài liệu liên quan: [Quản lý phiên làm việc](../../concepts/session.vi.md), [TUI (Giao diện terminal)](./tui.vi.md).
