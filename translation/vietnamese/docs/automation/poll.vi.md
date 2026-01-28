---
summary: "Gửi khảo sát (Poll) thông qua Gateway và CLI"
read_when:
  - Bạn muốn AI tạo các cuộc thăm dò ý kiến trên WhatsApp hoặc Discord
---

# Khảo sát (Polls)

Moltbot hỗ trợ việc gửi các cuộc thăm dò ý kiến (khảo sát) trực tiếp đến các ứng dụng nhắn tin.

## Các kênh hỗ trợ
- **WhatsApp**: Kênh phổ biến nhất.
- **Discord**: Hỗ trợ đầy đủ các tính năng.
- **MS Teams**: Hiển thị dưới dạng Thẻ tương tác (Adaptive Cards).

## Cách dùng qua dòng lệnh (CLI)

**Ví dụ gửi lên WhatsApp:**
```bash
moltbot message poll --target +84... \
  --poll-question "Trưa nay ăn gì?" --poll-option "Phở" --poll-option "Cơm" --poll-option "Bún"
```

**Ví dụ gửi lên Discord (Cho phép chọn nhiều phương án):**
```bash
moltbot message poll --channel discord --target channel:123... \
  --poll-question "Chọn phương án?" --poll-option "A" --poll-option "B" --poll-multi
```

## Các tham số chính
- `--poll-question`: Câu hỏi của cuộc khảo sát.
- `--poll-option`: Các phương án trả lời (Có thể lặp lại tham số này nhiều lần).
- `--poll-multi`: Cho phép người dùng chọn cùng lúc nhiều phương án.
- `--poll-duration-hours`: (Chỉ Discord) Thời gian khảo sát tồn tại (mặc định là 24 giờ).

## Sử dụng thông qua Agent
Agent của bạn có thể sử dụng công cụ `message` với hành động `poll` để tự động tạo khảo sát dựa trên nội dung trò chuyện.

---
Tài liệu liên quan: [Danh sách kênh](../channels/index.vi.md), [Công cụ Message](../tools/index.vi.md).
