---
summary: "Hành vi trò chuyện nhóm trên các nền tảng (WhatsApp/Telegram/Discord/Slack/Signal/iMessage/Teams)"
read_when:
  - Bạn muốn thay đổi cách Agent hoạt động trong nhóm hoặc thiết lập bộ lọc nhắc tên (@mention)
---

# Quản lý Nhóm (Groups)

Moltbot xử lý các cuộc trò chuyện nhóm một cách nhất quán trên tất cả các nền tảng: WhatsApp, Telegram, Discord, Slack, Signal, iMessage và Microsoft Teams.

## Giới thiệu cơ bản

Moltbot "sống" ngay trên chính tài khoản nhắn tin cá nhân của bạn. Không có một tài khoản robot riêng biệt nào trong WhatsApp. Nếu **bạn** ở trong một nhóm, Moltbot có thể nhìn thấy nhóm đó và phản hồi tại đó.

Hành vi mặc định:
- Các nhóm bị hạn chế (`groupPolicy: "allowlist"`).
- Việc phản hồi yêu cầu phải nhắc tên (@mention) trừ khi bạn tắt bộ lọc này.

Nói cách khác: Những người dùng có trong danh sách trắng (allowlist) có thể gọi Moltbot hoạt động bằng cách nhắc tên nó.

## Quy trình xử lý tin nhắn nhóm

Hệ thống sẽ kiểm tra theo thứ tự:
1. **Chính sách nhóm (`groupPolicy`)**: Có bị tắt (disabled) hay không?
2. **Danh sách trắng (Allowlist)**: Nhóm này có được phép hoạt động không?
3. **Bộ lọc nhắc tên (`requireMention`)**: Có yêu cầu nhắc tên không? Nếu có mà chưa nhắc tên, tin nhắn sẽ chỉ được lưu vào ngữ cảnh mà không phản hồi.

## Các kịch bản cấu hình phổ biến

| Mục tiêu | Cài đặt tương ứng |
|------|-------------|
| Cho phép mọi nhóm nhưng chỉ phản hồi khi được nhắc tên | `groups: { "*": { "requireMention": true } }` |
| Tắt hoàn toàn việc phản hồi trong nhóm | `groupPolicy: "disabled"` |
| Chỉ cho phép các nhóm cụ thể | `groups: { "<ID-nhóm>": { ... } }` (không dùng khóa `*`) |
| Chỉ có mình bạn mới có quyền gọi Bot trong nhóm | `groupPolicy: "allowlist"`, `groupAllowFrom: ["+1555..."]` |

## Đặc quyền của chủ sở hữu (Owner)

Chủ sở hữu của Bot có thể thay đổi chế độ kích hoạt trong từng nhóm bằng lệnh:
- `/activation mention`: Chỉ phản hồi khi được nhắc tên.
- `/activation always`: Phản hồi mọi lúc khi thấy cần thiết.

Người chủ được xác định thông qua tham số `allowFrom` trong cấu hình kênh. Các lệnh này phải được gửi dưới dạng tin nhắn độc lập.

## Ghi chú cho từng kênh

- **WhatsApp**: Xem chi tiết tại [Tin nhắn nhóm WhatsApp](./group-messages.vi.md).
- **Telegram**: Hỗ trợ các chủ đề (topics) trong nhóm Forum; mỗi chủ đề sẽ có một phiên làm việc riêng biệt.
- **iMessage**: Ưu tiên sử dụng `chat_id:<id>` khi thực hiện các quy tắc định tuyến hoặc cho phép nhóm. Bạn có thể xem danh sách chat bằng lệnh `moltbot imsg chats`.

---
Tài liệu liên quan: [Định tuyến kênh](./channel-routing.vi.md), [Cấu hình Gateway](../../gateway/configuration.vi.md).
