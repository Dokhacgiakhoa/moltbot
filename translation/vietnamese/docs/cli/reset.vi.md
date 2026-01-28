---
summary: "Tài liệu tham khảo lệnh `moltbot reset` (Khôi phục trạng thái/cấu hình mặc định)"
read_when:
  - Bạn muốn xóa sạch các cài đặt hiện tại để bắt đầu lại từ đầu
  - Bạn muốn xóa nhật ký trò chuyện và thông tin đăng nhập mà không gỡ cài đặt ứng dụng
---

# `moltbot reset`

Khôi phục lại cấu hình và trạng thái ban đầu của hệ thống (giữ nguyên bộ công cụ CLI).

## Ví dụ sử dụng

```bash
# Khởi chạy quy trình khôi phục có hướng dẫn
moltbot reset

# Xóa toàn bộ cấu hình, thông tin đăng nhập và các phiên trò chuyện mà không hỏi lại
moltbot reset --scope config+creds+sessions --yes --non-interactive

# Chạy thử để xem các file nào sẽ bị ảnh hưởng
moltbot reset --dry-run
```

**Các phạm vi khôi phục (Scopes):**
- `config`: Chỉ xóa file cấu hình JSON.
- `config+creds+sessions`: Xóa cấu hình, mã xác thực và toàn bộ lịch sử trò chuyện.
- `full`: Xóa toàn bộ dữ liệu ứng dụng trong thư mục `~/.clawdbot`.

---
Tài liệu liên quan: [Hướng dẫn thiết lập](./setup.vi.md), [Onboarding](../../start/onboarding.vi.md).
