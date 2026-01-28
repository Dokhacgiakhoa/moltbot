---
summary: "Quy tắc định tuyến theo từng kênh (WhatsApp, Telegram, Discord, Slack) và ngữ cảnh chia sẻ"
read_when:
  - Bạn muốn thay đổi cách Agent phản hồi trên các kênh chat khác nhau
---

# Kênh & Định tuyến (Channels & Routing)

Moltbot thực hiện định tuyến các câu trả lời **về đúng kênh nơi tin nhắn gốc được gửi đến**. Mô hình AI không tự chọn kênh; việc định tuyến là cố định và được kiểm soát bởi cấu hình hệ thống của bạn.

## Các thuật ngữ chính

- **Channel (Kênh)**: `whatsapp`, `telegram`, `discord`, `slack`, `webchat`, v.v.
- **AccountId**: Tài khoản cụ thể trên từng kênh.
- **AgentId**: Một thực thể Agent có không gian làm việc và bộ nhớ riêng biệt.
- **SessionKey**: Khóa định danh phiên làm việc, dùng để lưu trữ ngữ cảnh và kiểm soát việc chạy tuần tự.

## Cấu trúc khóa phiên làm việc (Session Key)

Tin nhắn trực tiếp (DM) thường gộp chung về phiên làm việc **chính (main)** của Agent:
- `agent:<agentId>:main` (Mặc định: `agent:main:main`)

Các nhóm và kênh cộng đồng sẽ được cách ly riêng:
- Nhóm: `agent:<agentId>:<channel>:group:<id>`
- Kênh/Phòng chat: `agent:<agentId>:<channel>:channel:<id>`

Ví dụ: `agent:main:whatsapp:group:120363424282127706@g.us`

## Quy tắc định tuyến (Cách chọn Agent)

Hệ thống sẽ chọn **duy nhất một Agent** cho mỗi tin nhắn đến dựa trên thứ tự ưu tiên:

1. **Khớp chính xác (Exact match)**: Dựa trên ID nhóm hoặc ID người dùng cụ thể.
2. **Khớp theo máy chủ (Guild match)**: Dành cho Discord.
3. **Khớp theo tài khoản (Account match)**: Dành cho các tài khoản cụ thể trong một ứng dụng.
4. **Khớp theo kênh (Channel match)**: Bất kỳ tin nhắn nào đến từ WhatsApp, Telegram, v.v.
5. **Agent mặc định**: Lựa chọn cuối cùng nếu không khớp các quy tắc trên (thường là `main`).

Agent được chọn sẽ quyết định không gian làm việc và lịch sử bộ nhớ nào sẽ được đem vào cuộc trò chuyện.

## Nhóm phát tin (Broadcast Groups)

Nhóm phát tin cho phép bạn chạy **nhiều Agent cùng lúc** cho cùng một cuộc trò chuyện. Điều này thường dùng trong các nhóm làm việc chung cần nhiều chuyên gia AI tư vấn cùng lúc.

Xem chi tiết tại: [Nhóm phát tin (Broadcast Groups)](../broadcast-groups.vi.md).

## Lưu trữ phiên làm việc

Dữ liệu được lưu tại thư mục trạng thái của hệ thống (mặc định là `~/.clawdbot`):
- `~/.clawdbot/agents/<agentId>/sessions/sessions.json`
- Lịch sử chat (transcripts) nằm ngay cạnh tệp cấu hình này dưới dạng JSONL.

---
Tài liệu liên quan: [Điều phối đa Agent](./multi-agent.vi.md), [Cấu hình Gateway](../gateway/configuration.vi.md).
