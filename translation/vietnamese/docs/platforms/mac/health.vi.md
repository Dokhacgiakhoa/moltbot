---
summary: "Cách ứng dụng macOS báo cáo trạng thái sức khỏe của Gateway và dịch vụ tin nhắn"
read_when:
  - Bạn muốn hiểu ý nghĩa các màu sắc của biểu tượng trên thanh menu
---

# Kiểm tra trạng thái trên macOS

Ứng dụng trên thanh menu cung cấp cái nhìn nhanh về việc liệu các kênh liên lạc (WhatsApp/Telegram) có đang hoạt động tốt hay không.

## Thanh Menu (Menu bar)
- **Dấu chấm trạng thái**:
  - **Xanh**: Đã kết nối và đang hoạt động tốt.
  - **Cam**: Đang thử kết nối lại.
  - **Đỏ**: Đã đăng xuất hoặc gặp lỗi nghiêm trọng.
- Dòng chữ phụ hiển thị chi tiết như "linked · auth 12m" (đã kết nối · xác thực cách đây 12 phút) hoặc lý do gây ra lỗi.
- Mục menu "Run Health Check" cho phép bạn kích hoạt kiểm tra ngay lập tức.

## Trong phần Cài đặt
- Tab **General**: Hiển thị thẻ sức khỏe với thông tin về thời gian xác thực, số lượng dữ liệu trong phiên, thời điểm kiểm tra cuối cùng và các mã lỗi nếu có.
- Tab **Channels**: Hiển thị chi tiết cho từng kênh (WhatsApp/Telegram) cùng với mã QR để đăng nhập hoặc nút đăng xuất.

## Cơ chế hoạt động
Ứng dụng sẽ tự động chạy lệnh `moltbot health --json` mỗi 60 giây một lần để lấy dữ liệu. Quá trình kiểm tra này chỉ kiểm tra thông tin xác thực mà không gửi bất kỳ tin nhắn thử nghiệm nào để tiết kiệm tài nguyên.

---
Tài liệu liên quan: [Môi trường chạy Gateway](./bundled-gateway.vi.md), [Xử lý lỗi](../../gateway/troubleshooting.vi.md).
