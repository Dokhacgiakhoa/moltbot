---
summary: "Phân tích chuyên sâu: Lưu trữ phiên, vòng đời hội thoại và cơ chế (tự động) nén dữ liệu"
read_when:
  - Bạn cần gỡ lỗi về ID phiên làm việc hoặc các tệp nhật ký hội thoại .jsonl
  - Bạn muốn thay đổi hành vi tự động nén (auto-compaction) của Bot
---

# Quản lý Phiên & Nén dữ liệu (Chuyên sâu)

Tài liệu này giải thích cách Moltbot quản lý các cuộc hội thoại từ đầu đến cuối.

## Hai lớp lưu trữ dữ liệu

Moltbot lưu trữ dữ liệu hội thoại tại hai nơi:

1) **Kho lưu trữ phiên (`sessions.json`)**:
   - Lưu trữ dưới dạng Bản đồ (Map) giữa `sessionKey` và các thông tin mô tả phiên.
   - Dung lượng nhỏ, có thể chỉnh sửa trực tiếp.
   - Theo dõi các thông tin như: ID phiên hiện tại, hoạt động cuối cùng, cài đặt riêng cho từng phiên, số lượng token đã dùng.

2) **Nhật ký hội thoại (`<sessionId>.jsonl`)**:
   - Lưu theo dạng nối thêm (append-only) với cấu trúc cây (mỗi tin nhắn có `id` và `parentId`).
   - Lưu nội dung thực tế của cuộc hội thoại, các lần gọi công cụ và các bản tóm tắt khi nén dữ liệu.
   - Được sử dụng để tái tạo lại ngữ cảnh cho AI trong các lượt chat tiếp theo.

## Vị trí lưu trữ trên ổ cứng
Thông thường các tệp này nằm trong thư mục người dùng:
- `~/.clawdbot/agents/<id-agent>/sessions/sessions.json`
- `~/.clawdbot/agents/<id-agent>/sessions/<id-phiên>.jsonl`

## Cơ chế Nén dữ liệu (Compaction)

Nén dữ liệu là quá trình tóm tắt các nội dung hội thoại cũ thành một bản tóm tắt duy nhất và chỉ giữ lại các tin nhắn mới nhất trong bộ nhớ của AI. 

**Khi nào nén dữ liệu tự động diễn ra?**
1. **Khi bị tràn bộ nhớ**: Mô hình AI báo lỗi ngữ cảnh đã đầy → Bot tự động nén dữ liệu và thử lại lệnh.
2. **Duy trì ngưỡng an toàn**: Sau mỗi lượt chat, nếu số lượng token vượt quá ngưỡng cho phép, Bot sẽ tự động thực hiện việc tóm tắt để giải phóng không gian bộ nhớ.

## Dọn dẹp trí nhớ trước khi nén (Memory flush)
Để đảm bảo AI không quên các thông tin quan trọng khi dữ liệu cũ bị nén đi, Moltbot thực hiện một lượt "dọn dẹp trí nhớ" ngầm. Bot sẽ bí mật tự nhắc mình ghi lại các sự kiện chính vào tệp trí nhớ (`memory.md`) trước khi quá trình nén thực sự bắt đầu. Quá trình này diễn ra âm thầm, người dùng sẽ không thấy Bot nhắn tin gì trong lúc này.

---
Tài liệu liên quan: [Khái niệm Phiên làm việc](../concepts/session.vi.md), [Khái niệm Nén dữ liệu](../concepts/compaction.vi.md).
