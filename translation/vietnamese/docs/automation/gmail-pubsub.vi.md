---
summary: "Tích hợp Gmail Pub/Sub vào Moltbot qua cổng Webhook bằng gogcli"
read_when:
  - Bạn muốn Bot tự động "thức dậy" khi có email mới đến Gmail
  - Bạn đang thiết lập hệ thống đẩy (push) thông báo từ Google Cloud
---

# Kết nối Gmail Pub/Sub đến Moltbot

Mục tiêu: Khi có email mới -> Google Pub/Sub gửi thông báo -> `gog` xử lý -> Gọi Webhook của Moltbot để Agent xử lý.

## Yêu cầu chuẩn bị
- Đã cài đặt và đăng nhập `gcloud` SDK.
- Đã cài đặt và cấp quyền cho `gog` (gogcli).
- Đã bật tính năng Hook trong Moltbot (xem [Webhooks](./webhook.vi.md)).
- Đã đăng nhập **Tailscale** (Khuyên dùng để có địa chỉ HTTPS công khai an toàn).

## Cấu hình mẫu cho Moltbot
Bạn cần thêm cấu hình sau vào `moltbot.json` để Bot biết cách xử lý khi nhận được dữ liệu từ Gmail:

```json5
{
  hooks: {
    enabled: true,
    presets: ["gmail"],
    mappings: [
      {
        match: { path: "gmail" },
        action: "agent",
        wakeMode: "now",
        name: "Gmail",
        messageTemplate: "Có email mới từ {{messages[0].from}}\nTiêu đề: {{messages[0].subject}}\nNội dung: {{messages[0].snippet}}",
        deliver: true,
        channel: "last"
      }
    ]
  }
}
```

## Thiết lập nhanh (Dùng Wizard)
Moltbot cung cấp lệnh hỗ trợ tự động thiết lập mọi đường dây kết nối (trên macOS):
```bash
moltbot webhooks gmail setup --account email-cua-ban@gmail.com
```

## Chạy trình theo dõi
Sau khi thiết lập, bạn có thể chạy lệnh sau để Bot bắt đầu lắng nghe các thông báo đẩy từ Gmail:
```bash
moltbot webhooks gmail run
```

## Lưu ý về bảo mật
- Luôn sử dụng mã Token cho Webhook để tránh người lạ gửi dữ liệu giả mạo.
- Các nội dung email từ bên ngoài mặc định sẽ được Bot xử lý trong môi trường an toàn (safety boundaries) để tránh các cuộc tấn công qua nội dung email (Prompt injection).

---
Tài liệu liên quan: [Hướng dẫn Webhooks](./webhook.vi.md), [Bảo mật](../gateway/security/index.vi.md).
