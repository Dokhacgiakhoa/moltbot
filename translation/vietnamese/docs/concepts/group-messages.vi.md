---
summary: "Hành vi và cấu hình cho việc xử lý tin nhắn nhóm trên WhatsApp (Mẫu nhắc tên được chia sẻ trên mọi nền tảng)"
read_when:
  - Bạn muốn cấu hình cách Agent hoạt động trong nhóm hoặc quy tắc nhắc tên (@mention)
---

# Tin nhắn nhóm (WhatsApp Web)

Mục tiêu: Cho phép Agent tham gia vào các nhóm WhatsApp, chỉ phản hồi khi được gọi tên (@-mention) và giữ cho các cuộc hội thoại trong nhóm hoàn toàn tách biệt với các cuộc trò chuyện cá nhân của bạn.

Lưu ý: Danh sách các mẫu nhắc tên (`mentionPatterns`) hiện được chia sẻ dùng chung cho cả Telegram, Discord, Slack và iMessage.

## Các tính năng đã triển khai

- **Chế độ kích hoạt**: Bao gồm `mention` (mặc định) hoặc `always`. 
  - `mention`: Yêu cầu phải nhắc tên Agent (thông qua @-mention thật của WhatsApp, hoặc các mẫu regex, hoặc số điện thoại của Agent).
  - `always`: Agent sẽ theo dõi tất cả tin nhắn nhưng chỉ phản hồi khi thấy có thông tin giá trị cần đóng góp; nếu không nó sẽ im lặng (trả về mã `NO_REPLY`).
  - Bạn có thể chuyển đổi giữa các chế độ này bằng lệnh `/activation`.
  
- **Chính sách nhóm (Group policy)**: Kiểm soát việc có chấp nhận tin nhắn từ nhóm hay không (`open` - mở cho tất cả, `disabled` - tắt hoàn toàn, hoặc `allowlist` - chỉ cho phép các nhóm nằm trong danh sách trắng).

- **Phiên làm việc riêng cho từng nhóm**: Các phiên làm việc nhóm hoàn toàn độc lập với các phiên DM cá nhân. Các lệnh như `/verbose on` hay `/think high` gửi trong nhóm sẽ chỉ có tác dụng trong nhóm đó, không ảnh hưởng đến bộ não của Agent ở nơi khác. Các lượt chạy tự động (heartbeats) sẽ không được thực hiện trong các nhóm chat để tránh làm phiền.

- **Nạp ngữ cảnh**: Các tin nhắn chờ trong nhóm chưa được phản hồi sẽ được gộp lại và chèn vào ngữ cảnh dưới nhãn `[Chat messages since your last reply - for context]` (Tin nhắn từ lần trả lời cuối - để lấy ngữ cảnh). Điều này giúp Agent nắm bắt được toàn bộ câu chuyện trong nhóm trước khi đưa ra câu trả lời chính thức cho tin nhắn hiện tại.

- **Định danh người gửi**: Mỗi đoạn hội thoại trong nhóm đều được đính kèm nhãn `[from: Tên người gửi (+Số điện thoại)]` ở cuối để Agent biết chính xác ai đang nói chuyện với mình.

## Ví dụ cấu hình (Mẫu nhắc tên)

Thêm khối `groupChat` vào file `moltbot.json` để Agent có thể nhận diện tên mình ngay cả khi ứng dụng chat lọc bỏ ký hiệu `@`:

```json
{
  "agents": {
    "list": [
      {
        "id": "main",
        "groupChat": {
          "historyLimit": 50,
          "mentionPatterns": [
            "@?moltbot",
            "\\+?15555550123"
          ]
        }
      }
    ]
  }
}
```

## Lệnh kích hoạt (Dành cho chủ sở hữu)

Sử dụng lệnh sau trong nhóm chat:
- `/activation mention`: Chỉ phản hồi khi được nhắc tên.
- `/activation always`: Luôn luôn lắng nghe và phản hồi khi cần.

Chỉ người chủ (được khai báo trong danh sách `allowFrom`) mới có quyền thay đổi các cài đặt này.

---
Tài liệu liên quan: [Cấu hình Nhóm (Groups)](./groups.vi.md), [Trạng thái hệ thống](../../cli/status.vi.md).
