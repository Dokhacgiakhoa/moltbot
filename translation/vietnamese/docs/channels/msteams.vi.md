---
summary: "Trạng thái hỗ trợ, khả năng và cấu hình cho bot Microsoft Teams"
read_when:
  - Bạn đang thiết lập kênh MS Teams qua Azure Bot
---
# Microsoft Teams (Plugin)

Trạng thái: Hỗ trợ tin nhắn văn bản, tệp đính kèm trong DM. Việc gửi tệp trong kênh nhóm yêu cầu thiết lập SharePoint và các quyền Microsoft Graph API nâng cao.

## Lưu ý quan trọng
Microsoft Teams được cung cấp dưới dạng **plugin** và không được cài đặt sẵn trong bộ lõi để giữ cho hệ thống nhẹ nhàng. Bạn cần cài đặt nó qua lệnh:
```bash
moltbot plugins install @moltbot/msteams
```

## Thiết lập nhanh (cho người mới)
1) Tạo một **Azure Bot** trên cổng thông tin Microsoft Azure (lấy App ID, Client Secret và Tenant ID).
2) Cấu hình địa chỉ Webhook trong Azure trỏ về địa chỉ Gateway của bạn (đường dẫn mặc định là `/api/messages`).
3) Tạo một gói ứng dụng Teams (manifest) chứa ID của bot và cài đặt nó vào Teams (của cá nhân hoặc tổ chức).
4) Cấu hình thông tin xác thực trên Moltbot.
5) Chạy Gateway. Các tin nhắn nhóm sẽ bị chặn theo mặc định cho đến khi bạn cấu hình danh sách trắng (allowlist).

## Mô hình phản hồi: Luồng tin nhắn (Threads) vs Bài đăng (Posts)
Teams có hai kiểu giao diện khác nhau:
- **Posts (Cổ điển)**: Các tin nhắn xuất hiện dưới dạng thẻ, phản hồi nằm gọn bên dưới. (Khuyên dùng chế độ `thread`).
- **Threads (Giống Slack)**: Tin nhắn hiển thị theo dòng thời gian liên tục. (Khuyên dùng chế độ `top-level`).
Moltbot cho phép bạn cấu hình chế độ phản hồi riêng cho từng kênh để phù hợp với giao diện của nó.

## Quyền hạn và Microsoft Graph
- **Chỉ dùng RSC (Mặc định)**: Bot có thể đọc/gửi văn bản và nhận tệp trong DM. Không thể tải nội dung hình ảnh trong kênh nhóm.
- **Dùng thêm Microsoft Graph API**: Cho phép bot tải hình ảnh, tệp đính kèm từ SharePoint/OneDrive và đọc lịch sử tin nhắn cũ khi bot offline.

## Cấu hình mẫu
```json5
{
  channels: {
    msteams: {
      enabled: true,
      appId: "<APP_ID>",
      appPassword: "<APP_PASSWORD>",
      tenantId: "<TENANT_ID>",
      webhook: { port: 3978, path: "/api/messages" },
      dm: { policy: "pairing" }
    }
  }
}
```

---
Tài liệu liên quan: [Plugin](../../plugin.vi.md), [Thẻ thích ứng (Adaptive Cards)](https://adaptivecards.io/).
