---
summary: "Kế hoạch: Xây dựng một bộ SDK và môi trường chạy Plugin chuẩn hóa cho tất cả các kênh nhắn tin"
---

# Tái cấu trúc SDK và Môi trường chạy Plugin

## Mục tiêu
Mục tiêu của kế hoạch này là biến mọi kết nối kênh nhắn tin (WhatsApp, Telegram, v.v.) thành một plugin sử dụng chung một bộ API ổn định. Điều này giúp:
- Các plugin không còn phải can thiệp trực tiếp vào mã nguồn cốt lõi của hệ thống.
- Việc cập nhật Moltbot trở nên an toàn hơn vì các plugin chỉ giao tiếp qua một lớp trung gian (SDK).
- Người dùng bên ngoài dễ dàng viết thêm các kênh nhắn tin mới cho Bot.

## Kiến trúc mục tiêu (Hai lớp)

### 1. Bộ SDK Plugin (Dành cho nhà phát triển)
Bao gồm các kiểu dữ liệu, các công cụ hỗ trợ cấu hình và các hàm tiện ích. Đây là bộ công cụ giúp bạn định nghĩa plugin của mình sẽ trông như thế nào và nó cần những gì.

### 2. Môi trường chạy Plugin (Runtime)
Đây là lớp thực thi, cho phép các plugin truy cập vào các tính năng của Moltbot như:
- Gửi và nhận tin nhắn.
- Tải và xử lý hình ảnh/video.
- Kiểm tra quyền hạn và vai trò của người dùng.
- Ghi nhật ký (logs) và quản lý trạng thái.

## Lộ trình thực hiện
- **Giai đoạn 0**: Giới thiệu bộ SDK `@clawdbot/plugin-sdk`.
- **Giai đoạn 1**: Dọn dẹp các plugin hiện có để chúng bắt đầu sử dụng SDK mới.
- **Giai đoạn 2**: Chuyển đổi các kênh nhắn tin nhẹ (như BlueBubbles, Zalo) sang hệ thống mới.
- **Giai đoạn 3**: Chuyển đổi các kênh phức tạp hơn (như MS Teams).
- **Giai đoạn 4**: Biến các tính năng cốt lõi như iMessage thành một plugin hoàn chỉnh.
- **Giai đoạn 5**: Áp dụng các quy tắc kiểm tra nghiêm ngặt để đảm bảo không có sự can thiệp trái phép vào mã nguồn lõi.

## Tiêu chí thành công
- Tất cả các kết nối kênh nhắn tin đều là plugin độc lập.
- Không có bất kỳ dòng mã nào của plugin phải gọi trực tiếp vào thư mục mã nguồn chính của Moltbot.
- Các plugin mới có thể được phát triển và cập nhật mà không cần quan tâm đến mã nguồn bên trong của Bot.

---
Tài liệu liên quan: [Hệ thống Plugin](../plugins/index.vi.md), [Các kênh nhắn tin](../../channels/index.vi.md).
