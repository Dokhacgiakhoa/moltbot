---
summary: "Quy tắc quản lý phiên làm việc, khóa phiên và cơ chế lưu trữ nội dung chat"
read_when:
  - Bạn muốn thay đổi cách hệ thống xử lý hoặc lưu trữ các phiên hội thoại
---

# Quản lý phiên làm việc (Session Management)

Moltbot coi **một phiên chat cá nhân (DM) cho mỗi Agent** là phiên làm việc chính. Các cuộc trò chuyện cá nhân sẽ được gộp chung vào một phiên để đảm bảo tính liên tục, trong khi các nhóm hoặc kênh chat sẽ có các khóa phiên riêng biệt để tránh nhầm lẫn dữ liệu.

## Gateway là nguồn dữ liệu gốc
Tất cả trạng thái của phiên làm việc đều do **Gateway quản lý**. Các ứng dụng giao diện (như ứng dụng Mac hay WebChat) phải truy vấn dữ liệu từ Gateway thay vì tự đọc các tệp cục bộ.

- Khi chạy ở chế độ từ xa (remote mode), lịch sử chat của bạn nằm trên máy chủ chạy Gateway, không phải trên máy tính cá nhân.
- Các thông số về số lượng Token tiêu thụ cũng được lấy trực tiếp từ Gateway.

## Vị trí lưu trữ dữ liệu
Dữ liệu phiên làm việc được lưu trên máy chủ chạy Gateway tại đường dẫn:
- Tệp quản lý chung: `~/.clawdbot/agents/<agentId>/sessions/sessions.json`
- Lịch sử chat chi tiết: `~/.clawdbot/agents/<agentId>/sessions/<ID-phiên>.jsonl`

## Vòng đời của một phiên làm việc

- **Chính sách đặt lại (Reset)**: Các phiên làm việc sẽ được dùng đi dùng lại cho đến khi hết hạn.
- **Đặt lại hàng ngày**: Mặc định là vào **4:00 sáng theo giờ địa phương của máy chủ Gateway**. Nếu tin nhắn mới đến sau thời điểm này, hệ thống sẽ tự động tạo một phiên làm việc mới.
- **Đặt lại khi không hoạt động (Idle reset)**: Bạn có thể cấu hình để hệ thống tự làm mới phiên sau một khoảng thời gian bạn không nhắn tin (ví dụ: sau 2 tiếng im lặng).
- **Lệnh đặt lại thủ công**: Bạn có thể gõ lệnh `/new` hoặc `/reset` trong ô chat để bắt đầu một phiên làm việc hoàn toàn mới ngay lập tức. Lệnh `/new <model>` còn cho phép bạn đổi sang một mô hình AI khác cho phiên mới đó.

## Kiểm tra trạng thái phiên
Bạn có thể dùng các lệnh sau:
- `moltbot status`: Xem các phiên làm việc gần đây và vị trí lưu trữ.
- Gõ `/status` trong ô chat: Xem Agent có đang hoạt động không, cửa sổ ngữ cảnh đã dùng bao nhiêu phần trăm.
- Gõ `/stop` để ngắt ngay lập tức lượt chạy hiện tại của Agent và hủy các tin nhắn đang chờ trong hàng đợi.
- Gõ `/compact` để tóm tắt các nội dung cũ và giải phóng bộ nhớ cho cửa sổ ngữ cảnh.

---
Tài liệu liên quan: [Cấu hình hệ thống](../../gateway/configuration.vi.md), [Nén ngữ cảnh](./compaction.vi.md), [Cắt tỉa phiên](./session-pruning.vi.md).
