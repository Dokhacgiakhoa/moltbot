---
summary: "Kế hoạch củng cố lệnh cron.add, đồng bộ sơ đồ và cải thiện giao diện quản lý tác vụ định kỳ"
owner: "moltbot"
status: "hoàn thành"
last_updated: "2026-01-05"
---

# Củng cố lệnh Thêm tác vụ định kỳ (Cron Add Hardening)

## Bối cảnh
Các nhật ký lỗi của Gateway cho thấy lệnh `cron.add` thường xuyên thất bại do thiếu hoặc sai các tham số (như `sessionTarget`, `wakeMode`, `payload`, hoặc định dạng lịch trình `schedule`). Điều này cho thấy các công cụ AI khi gọi lệnh đang tạo ra các dữ liệu không chuẩn xác. Ngoài ra, còn có sự không đồng nhất về danh sách các nhà cung cấp (providers) giữa mã nguồn, giao diện và dòng lệnh.

## Mục tiêu
- Ngừng các lỗi `INVALID_REQUEST` của lệnh `cron.add` bằng cách tự động chuẩn hóa dữ liệu đầu vào.
- Đồng bộ danh sách các nhà cung cấp tác vụ định kỳ trên toàn bộ hệ thống (Gateway, CLI, UI).
- Làm cho sơ đồ cấu hình của công cụ AI trở nên rõ ràng hơn để AI có thể tạo ra các lệnh chính xác.
- Sửa lỗi hiển thị số lượng tác vụ trong bảng điều khiển.

## Những gì đã thay đổi
- Lệnh `cron.add` và `cron.update` hiện đã có khả năng tự suy luận các trường thông tin bị thiếu (ví dụ: loại lịch trình).
- Cấu trúc dữ liệu mà AI nhận được đã khớp hoàn toàn với cấu trúc của Gateway, giúp giảm thiểu lỗi khi AI tự tạo lệnh.
- Danh sách các nhà cung cấp (Discord, Slack, Signal, iMessage) hiện đã được hiển thị đồng nhất trên mọi giao diện.
- Bảng điều khiển hiện đã hiển thị chính xác số lượng tác vụ đang chạy.

## Hành vi hiện tại
- **Chuẩn hóa**: Nếu dữ liệu gửi đến bị đóng gói sai cách, hệ thống sẽ tự động mở gói và sửa lại.
- **Giá trị mặc định**: Các tham số quan trọng nhưng bị thiếu sẽ được điền các giá trị mặc định an toàn.

---
Tài liệu liên quan: [Tác vụ định kỳ (Cron jobs)](../../automation/cron-jobs.vi.md), [Bảng điều khiển](../../web/dashboard.vi.md).
