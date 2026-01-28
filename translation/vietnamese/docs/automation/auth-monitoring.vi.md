---
summary: "Theo dõi thời gian hết hạn OAuth cho các nhà cung cấp mô hình AI"
read_when:
  - Bạn muốn thiết lập hệ thống cảnh báo khi sắp hết hạn đăng nhập
  - Bạn đang tự động hóa việc kiểm tra làm mới OAuth cho Claude Code / Codex
---

# Theo dõi xác thực (Auth monitoring)

Moltbot cung cấp thông tin về tình trạng hết hạn OAuth thông qua lệnh `moltbot models status`. Bạn có thể sử dụng lệnh này để tự động hóa việc gửi cảnh báo.

## Cách khuyên dùng: Kiểm tra qua CLI
Lệnh sau đây có thể sử dụng trong các kịch bản cron hoặc systemd mà không cần thêm script phụ trợ:

```bash
moltbot models status --check
```

**Các mã trả về (Exit codes):**
- `0`: Mọi thứ bình thường (OK).
- `1`: Đã hết hạn hoặc thiếu thông tin đăng nhập.
- `2`: Sắp hết hạn (trong vòng 24 giờ tới).

## Các kịch bản tùy chọn (Dành cho điện thoại hoặc hệ thống chuyên sâu)
Các tệp tin nằm trong thư mục `scripts/` hỗ trợ thêm các quy trình nâng cao:
- `scripts/auth-monitor.sh`: Chạy định kỳ để gửi cảnh báo qua ntfy hoặc điện thoại.
- `scripts/mobile-reauth.sh`: Quy trình đăng nhập lại thông qua kết nối SSH trên điện thoại.
- `scripts/termux-quick-auth.sh`: Tiện ích (widget) trên Android (Termux) để xem trạng thái nhanh.

Nếu bạn không cần tự động hóa trên điện thoại, bạn có thể bỏ qua các kịch bản này.

---
Tài liệu liên quan: [Cài đặt SSH trên di động](../gateway/remote.vi.md), [Xử lý lỗi](../gateway/troubleshooting.vi.md).
