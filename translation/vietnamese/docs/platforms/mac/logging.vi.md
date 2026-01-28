---
summary: "Hệ thống nhật ký của Moltbot: Ghi tệp chẩn đoán xoay vòng và quyền riêng tư của nhật ký hệ thống"
read_when:
  - Bạn cần thu thập nhật ký lỗi trên máy Mac hoặc điều tra dữ liệu riêng tư
---

# Hệ thống Nhật ký (macOS)

## Nhật ký chẩn đoán xoay vòng (Rolling diagnostics)
Moltbot có thể ghi nhật ký hoạt động vào một tệp tin cục bộ để phục vụ việc chẩn đoán lỗi lâu dài.

- **Bật tính năng**: Mở bảng **Debug → Logs → App logging → "Write rolling diagnostics log (JSONL)"**.
- **Vị trí tệp**: `~/Library/Logs/Moltbot/diagnostics.jsonl`.
- **Cơ chế**: Tệp sẽ tự động "xoay vòng" khi đạt kích thước giới hạn, các tệp cũ sẽ được đánh số thứ tự `.1`, `.2`, v.v.

**Lưu ý**: Tính năng này mặc định là **Tắt**. Chỉ nên bật khi bạn đang chủ động tìm lỗi vì tệp nhật ký có thể chứa thông tin nhạy cảm.

## Quyền riêng tư của Nhật ký Hệ thống (Unified logging)
Trên macOS, nhật ký hệ thống thường tự động ẩn (redact) các dữ liệu nhạy cảm. Để xem được đầy đủ chi tiết khi gỡ lỗi, bạn cần tạo một tệp cấu hình đặc biệt trong hệ thống.

**Cách bật xem dữ liệu riêng tư cho Moltbot:**
Bạn cần chạy lệnh sau trong Terminal với quyền `sudo`:
```bash
# Lệnh cài đặt cấu hình cho bot.molt
sudo install -m 644 -o root -g wheel /tmp/bot.molt.plist /Library/Preferences/Logging/Subsystems/bot.molt.plist
```

Sau khi gỡ lỗi xong, hãy nhớ xóa tệp cấu hình này để đảm bảo an toàn thông tin cá nhân (số điện thoại, nội dung tin nhắn).

---
Tài liệu liên quan: [Xử lý sự cố](../../gateway/troubleshooting.vi.md), [Thiết lập nhà phát triển](./dev-setup.vi.md).
