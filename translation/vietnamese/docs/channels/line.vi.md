---
summary: "Thiết lập plugin LINE Messaging API, cấu hình và cách sử dụng"
read_when:
  - Bạn muốn kết nối Moltbot với ứng dụng LINE
---
# LINE (Plugin)

Moltbot kết nối với LINE thông qua **LINE Messaging API**. Plugin này đóng vai trò là một bộ tiếp nhận Webhook trên Gateway, sử dụng "Channel access token" và "Channel secret" của bạn để xác thực.

## Cài đặt Plugin
Trước tiên, bạn cần cài đặt plugin LINE cho Moltbot:
```bash
moltbot plugins install @moltbot/line
```

## Các bước thiết lập
1. Tạo một tài khoản LINE Developers và truy cập Console tại: [developers.line.biz](https://developers.line.biz/console/).
2. Tạo một nhà cung cấp (Provider) và thêm một kênh **Messaging API**.
3. Sao chép **Channel access token** và **Channel secret** từ phần cài đặt kênh.
4. Bật tính năng **Use webhook** trong cài đặt Messaging API.
5. Thiết lập Webhook URL tới Gateway của bạn (Yêu cầu HTTPS):
   `https://gateway-cua-ban/line/webhook`

## Cấu hình Moltbot.json
Cấu hình tối thiểu:
```json5
{
  channels: {
    line: {
      enabled: true,
      channelAccessToken: "MÃ_ACCESS_TOKEN_CỦA_BẠN",
      channelSecret: "MÃ_SECRET_CỦA_BẠN",
      dmPolicy: "pairing"
    }
  }
}
```

## Kiểm soát quyền truy cập
- **Tin nhắn trực tiếp (DM)**: Mặc định sử dụng cơ chế ghép đôi (`pairing`). Người dùng mới phải nhập mã ghép đôi trước khi có thể ra lệnh cho bot.
- **Danh sách trắng (Allowlist)**: Bạn có thể chỉ định chính xác các ID người dùng hoặc nhóm được phép tương tác với bot để đảm bảo an toàn.

## Tính năng tin nhắn phong phú
Moltbot hỗ trợ gửi các loại tin nhắn đặc thù của LINE như:
- **Flex Cards**: Các thẻ thông tin có thể tùy chỉnh giao diện phức tạp.
- **Quick Replies**: Các nút bấm phản hồi nhanh thường dùng cho các lựa chọn "Có/Không" hoặc menu lệnh.
- **Gửi vị trí**: Gửi tọa độ bản đồ trực tiếp cho AI.

## Giải quyết sự cố
- **Xác minh Webhook thất bại**: Kiểm tra lại xem Webhook URL có phải là HTTPS không và mã `channelSecret` đã chính xác chưa.
- **Không nhận được tin nhắn**: Đảm bảo cổng mạng trên máy chủ của bạn đã được mở và không bị chặn bởi tường lửa.

---
Tài liệu liên quan: [Cơ chế Ghép đôi](../../start/pairing.vi.md), [Cấu hình Plugin](../../plugin.vi.md).
