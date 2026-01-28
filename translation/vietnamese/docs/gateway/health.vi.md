---
summary: "Các bước kiểm tra sức khỏe và kết nối của các kênh nhắn tin"
read_when:
  - Bạn muốn kiểm tra xem WhatsApp/Telegram đã được kết nối thành công chưa
---

# Kiểm tra sức khỏe (Health Checks)

Hướng dẫn ngắn gọn để kiểm tra kết nối các kênh nhắn tin một cách chính xác.

## Các lệnh kiểm tra nhanh
- `moltbot status`: Xem tóm tắt nhanh: Gateway có đang chạy không, thời gian đăng nhập của các kênh, số lượng phiên chat gần đây.
- `moltbot status --all`: Chẩn đoán đầy đủ (dạng văn bản thuần, an toàn để dán lên các diễn đàn hỗ trợ).
- `moltbot health --json`: Yêu cầu Gateway đang chạy báo cáo chi tiết về tình trạng sức khỏe của các thành phần bên trong.
- Gửi lệnh `/status` từ WhatsApp: Bot sẽ trả lời tình trạng hiện tại của nó ngay trong ô chat.

## Chẩn đoán chuyên sâu
- **Thông tin đăng nhập**: Kiểm tra tệp `creds.json` trong thư mục `~/.clawdbot/credentials/whatsapp/` xem thời gian cập nhật có mới không.
- **Quy trình liên kết lại (Relink)**: Nếu bạn thấy lỗi `logged out` hoặc mã lỗi từ 409 đến 515 trong nhật ký, hãy dùng lệnh sau để đăng nhập lại:
  ```bash
  moltbot channels logout && moltbot channels login --verbose
  ```

## Khi có lỗi xảy ra
- **Gateway không thể truy cập**: Hãy khởi động nó bằng lệnh `moltbot gateway`.
- **Không nhận được tin nhắn**: 
  - Đảm bảo điện thoại của bạn đang trực tuyến.
  - Kiểm tra xem số điện thoại người gửi đã nằm trong danh sách được phép chưa (`allowFrom`).
  - Đối với nhóm chat, hãy kiểm tra xem bạn đã cấu hình nhãn nhắc tên (@mention) đúng chưa.

---
Tài liệu liên quan: [Lệnh Doctor](./doctor.vi.md), [Xử lý lỗi](./troubleshooting.vi.md).
