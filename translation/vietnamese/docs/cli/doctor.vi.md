---
summary: "Tài liệu tham khảo lệnh `moltbot doctor` (Kiểm tra sức khỏe + Hướng dẫn sửa lỗi)"
read_when:
  - Bạn gặp vấn đề về kết nối, xác thực và muốn hệ thống tự động kiểm tra và gợi ý cách sửa
  - Bạn vừa cập nhật Moltbot và muốn kiểm tra lại tính ổn định
---

# `moltbot doctor`

Lệnh này thực hiện các bước kiểm tra sức khỏe và đưa ra các giải pháp sửa lỗi nhanh cho Gateway cũng như các kênh truyền thông.

Tài liệu liên quan:
- Khắc phục sự cố: [Sửa lỗi Gateway](../gateway/troubleshooting.vi.md)
- Kiểm tra bảo mật: [Bảo mật](../gateway/security/index.vi.md)

## Ví dụ sử dụng

```bash
# Kiểm tra tổng quát
moltbot doctor

# Tự động thực hiện các bước sửa lỗi
moltbot doctor --repair

# Kiểm tra sâu vào các dịch vụ hệ thống
moltbot doctor --deep
```

## Một số lưu ý quan trọng:
- **Tương tác**: Các gợi ý sửa lỗi (như keychain hoặc OAuth) chỉ xuất hiện khi bạn chạy lệnh này trực tiếp trong terminal. Nếu chạy ngầm, hệ thống sẽ chỉ áp dụng các bước chuyển đổi (migration) an toàn.
- **Dự phòng**: Khi bạn sử dụng `--repair` (hoặc `--fix`), một bản sao lưu cấu hình sẽ được tạo tại `~/.clawdbot/moltbot.json.bak` trước khi thực hiện thay đổi.

---
Tài liệu liên quan: [Trạng thái hệ thống](./status.vi.md).
