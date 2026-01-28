---
summary: "Các mô hình bảo mật được máy kiểm chứng cho những quy trình rủi ro nhất của Moltbot"
read_when:
  - Bạn là chuyên gia bảo mật và muốn biết hệ thống được bảo vệ như thế nào ở mức độ toán học
---

# Kiểm chứng hình thức (Mô hình bảo mật)

Trang này theo dõi các **mô hình bảo mật hình thức** của Moltbot (hiện đang sử dụng ngôn ngữ TLA+).

**Mục tiêu**: Cung cấp một lập luận đã được máy kiểm chứng rằng Moltbot luôn thực thi đúng các chính sách bảo mật đã đề ra (như cách ly phiên chat, kiểm soát công cụ và an toàn cấu hình) dưới các giả định nhất định.

## Những gì chúng tôi đã thực hiện
Hiện tại, chúng tôi có các bộ kiểm tra hồi quy cho các quy trình sau:
- **Tiếp xúc mạng của Gateway**: Kiểm chứng rằng việc mở cổng ra internet mà không có mật khẩu sẽ bị coi là rủi ro và mã xác thực có thể ngăn chặn hiệu quả các cuộc tấn công.
- **Quy trình chạy lệnh trên thiết bị (Nodes.run)**: Đảm bảo các lệnh chỉ được thực thi khi có sự cho phép rõ ràng và danh sách trắng được tuân thủ.
- **Lưu trữ ghép nối (Pairing store)**: Kiểm tra các quy tắc về thời gian hết hạn và giới hạn số lượng yêu cầu đang chờ để tránh tấn công từ chối dịch vụ (DoS).
- **Cách ly luồng tin nhắn**: Đảm bảo tin nhắn của những người dùng khác nhau không bao giờ bị trộn lẫn vào cùng một phiên hội thoại.

## Lưu ý quan trọng
- Đây là các **mô hình toán học**, không phải bản thân mã nguồn TypeScript. Do đó vẫn có thể có sự sai lệch nhỏ giữa lý thuyết và thực tế triển khai.
- Các kết quả "xanh" (vượt qua kiểm tra) chỉ đúng trong phạm vi các giả định và môi trường đã được mô phỏng.

Nếu bạn muốn tự mình chạy lại các bài kiểm tra này, bạn có thể tham khảo mã nguồn các mô hình bảo mật tại kho lưu trữ công khai trên GitHub của dự án.

---
Tài liệu liên quan: [Bảo mật](./index.vi.md), [Giao thức Gateway](../protocol.vi.md).
