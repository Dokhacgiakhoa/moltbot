---
summary: "Phê duyệt thực thi lệnh, danh sách trắng và các cảnh báo an toàn"
read_when:
  - Bạn muốn thiết lập cơ chế kiểm soát khi AI chạy lệnh trên máy tính
---
# Phê duyệt thực thi lệnh (Exec approvals)

Cơ chế này đóng vai trò như một **hàng rào bảo vệ (guardrail)** khi bạn cho phép AI (đang trong môi trường cô lập) thực thi các lệnh trên máy tính thật của bạn. Đây là chốt chặn an toàn cuối cùng: lệnh chỉ được chạy khi cả chính sách, danh sách trắng và sự đồng ý của bạn đều khớp nhau.

## Các mức độ chính sách an toàn
- **Chặn hoàn toàn (deny)**: Không cho phép AI chạy bất kỳ lệnh nào trên máy thật.
- **Danh sách trắng (allowlist)**: Chỉ cho phép các lệnh nằm trong danh sách bạn đã phê duyệt từ trước.
- **Toàn quyền (full)**: Cho phép AI chạy mọi lệnh (Tương đương với chế độ đặc quyền).

## Cách hoạt động của danh sách trắng
Danh sách trắng được quản lý **riêng biệt cho từng Agent**. Điều này giúp ngăn chặn việc một AI làm việc này có thể vô tình chạy các lệnh của AI khác.
Bạn có thể dùng các mẫu (patterns) dạng glob như:
- `~/.local/bin/*`: Cho phép chạy mọi tệp trong thư mục bin cục bộ.
- `/usr/bin/grep`: Chỉ cho phép duy nhất lệnh tìm kiếm grep.

## Quy trình phê duyệt
Khi AI cần chạy một lệnh chưa được cấp quyền sẵn, một thông báo sẽ hiện ra trên ứng dụng điều khiển (ví dụ trên macOS hoặc trang Dashboard). Bạn có các lựa chọn:
1. **Chỉ chạy một lần (Allow once)**: Cho phép lệnh này chạy ngay bây giờ.
2. **Luôn cho phép (Always allow)**: Chạy lệnh và tự động thêm nó vào danh sách trắng để sau này không hỏi lại nữa.
3. **Từ chối (Deny)**: Chặn lệnh thực thi.

## Phê duyệt từ xa qua ứng dụng Chat
Bạn thậm chí có thể cấu hình để Moltbot gửi yêu cầu phê duyệt tới Telegram hoặc Slack của bạn. Để đồng ý, bạn chỉ cần nhắn:
- `/approve <mã_id> allow-once`

---
Tài liệu liên quan: [Công cụ thực thi lệnh](./exec.vi.md), [Chế độ đặc quyền](./elevated.vi.md).
