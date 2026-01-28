---
summary: "Tái cấu trúc việc phản chiếu phiên tin nhắn đi: Đảm bảo tin nhắn được lưu đúng vào cuộc hội thoại tương ứng"
---

# Tái cấu trúc Phản chiếu Phiên tin nhắn đi (Outbound Session Mirroring)

## Bối cảnh
Trước đây, các tin nhắn mà Bot gửi đi đôi khi bị lưu sai vào phiên làm việc (session) hiện tại của Agent thay vì lưu vào đúng cuộc hội thoại với người nhận. Điều này dẫn đến việc lịch sử chat bị xáo trộn hoặc không hiển thị đúng đối với các liên hệ mới.

## Mục tiêu
- Luôn phản chiếu các tin nhắn gửi đi vào đúng phiên làm việc của kênh nhận tin.
- Tự động tạo các bản ghi phiên làm việc nếu nó chưa tồn tại khi gửi tin nhắn lần đầu.
- Đảm bảo việc phân loại theo chủ đề (threads/topics) trên Slack, Discord, Telegram luôn đồng nhất.

## Những gì đã thay đổi
- Hệ thống điều hướng tin nhắn đi mới hiện đã có khả năng xác định chính xác phiên làm việc dựa trên thông tin người nhận.
- Các công cụ gửi tin nhắn không còn tự ý lưu trữ dữ liệu, mà chuyển quyền điều khiển cho một dịch vụ tập trung để đảm bảo tính nhất quán.
- Hỗ trợ đầy đủ cho các kênh: Slack, Discord, Telegram, Zalo, WhatsApp, và nhiều kênh khác.

## Quy tắc xử lý cụ thể
- **Slack**: Các tin nhắn trả lời trong luồng (threads) sẽ được lưu vào đúng phiên của luồng đó.
- **Discord**: Các kênh chủ đề cũng được phân loại chính xác.
- **Telegram**: Các chủ đề (topics) trong nhóm chat được lưu riêng biệt dựa trên ID của chủ đề.
- **Zalo**: Phân biệt rõ ràng giữa tin nhắn cá nhân và tin nhắn nhóm.

## Kết quả
Lịch sử trò chuyện của bạn sẽ luôn chính xác và đầy đủ, bất kể tin nhắn đó là do bạn gửi cho Bot hay do Bot tự động gửi cho bạn.

---
Tài liệu liên quan: [Hệ thống Phiên làm việc](../../concepts/sessions.vi.md), [Nhật ký hội thoại](../../reference/session-management-compaction.vi.md).
