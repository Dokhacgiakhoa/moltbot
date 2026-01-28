---
summary: "Tài liệu tham khảo lệnh `moltbot webhooks` (Công cụ hỗ trợ Webhook + Gmail Pub/Sub)"
read_when:
  - Bạn muốn kết nối các sự kiện từ Gmail vào Moltbot
---

# `moltbot webhooks`

Cung cấp các công cụ hỗ trợ cho Webhook và các tích hợp bên thứ ba (như Gmail Pub/Sub).

Tài liệu liên quan:
- Webhooks: [Tổng quan Webhook](../../automation/webhook.vi.md)
- Gmail Pub/Sub: [Tích hợp Gmail](../../automation/gmail-pubsub.vi.md)

## Tích hợp Gmail

```bash
# Thiết lập tài khoản Gmail kết nối với Google Cloud Pub/Sub
moltbot webhooks gmail setup --account email_cua_ban@gmail.com

# Chạy trình lắng nghe sự kiện từ Gmail
moltbot webhooks gmail run
```

Hãy xem thêm [Tài liệu hướng dẫn Gmail Pub/Sub](../../automation/gmail-pubsub.vi.md) để biết các bước cấu hình phía Google Cloud Console trước khi chạy các lệnh này.
