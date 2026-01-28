---
summary: "Lệnh Doctor: Kiểm tra sức khỏe, chuyển đổi cấu hình và các bước sửa lỗi"
read_when:
  - Bạn gặp lỗi không thể khởi động Gateway do cấu hình cũ hoặc sai sót hệ thống
---

# Lệnh Doctor (Chẩn đoán & Sửa lỗi)

`moltbot doctor` là công cụ sửa chữa và chuyển đổi dữ liệu của Moltbot. Lệnh này giúp khắc phục các tệp cấu hình cũ, kiểm tra sức khỏe hệ thống và đưa ra các bước sửa lỗi cụ thể.

## Bắt đầu nhanh

```bash
moltbot doctor
```

### Chế độ tự động
```bash
moltbot doctor --yes
```
Tự động chấp nhận các đề xuất sửa chữa mà không cần hỏi lại (bao gồm cả việc khởi động lại dịch vụ nếu cần).

```bash
moltbot doctor --repair
```
Chỉ áp dụng các sửa chữa được khuyên dùng một cách an toàn.

## Lệnh Doctor làm những gì?

1. **Kiểm tra sức khỏe**: Đảm bảo Gateway đang chạy và có thể phản hồi.
2. **Chuẩn hóa cấu hình**: Nếu bạn đang dùng tệp cấu hình từ phiên bản cũ, lệnh này sẽ tự động chuyển đổi các trường dữ liệu sang định dạng mới nhất.
3. **Di chuyển dữ liệu cũ**: Tự động chuyển các tệp lịch sử chat (sessions) và thông tin đăng nhập từ các thư mục cũ sang cấu hình đa Agent mới.
4. **Kiểm tra quyền truy cập**: Đảm bảo Moltbot có quyền đọc/ghi vào các thư mục cần thiết.
5. **Kiểm tra tài khoản AI**: Thông báo nếu các Token (như của Anthropic) sắp hết hạn hoặc bị lỗi.
6. **Xử lý xung đột cổng**: Chẩn đoán lý do tại sao không thể mở cổng 18789 (ví dụ: có một bản Moltbot khác đang chạy).
7. **Cảnh báo bảo mật**: Nhắc nhở nếu bạn đang để cấu hình quá lỏng lẻo (ví dụ: cho phép bất kỳ ai cũng có thể nhắn tin cho Bot).

## Khi nào nên dùng lệnh này?
- Sau khi bạn vừa nâng cấp Moltbot lên phiên bản mới.
- Khi Gateway báo lỗi "Unknown configuration keys".
- Khi bạn thấy Bot không phản hồi trên WhatsApp/Telegram như bình thường.
- Khi bạn muốn dọn dẹp các tệp dữ liệu rác của các phiên bản cũ.

---
Tài liệu liên quan: [Cấu hình hệ thống](./configuration.vi.md), [Xử lý lỗi](./troubleshooting.vi.md).
