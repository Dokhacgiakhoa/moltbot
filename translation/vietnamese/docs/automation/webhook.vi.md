---
summary: "Cổng nhận Webhook để đánh thức Bot và chạy Agent cô lập"
read_when:
  - Bạn muốn kết nối các hệ thống bên ngoài (như GitHub, Jenkins, Email) vào Moltbot
---

# Webhooks

Moltbot Gateway cung cấp một cổng HTTP nhỏ để nhận các tín hiệu kích hoạt từ bên ngoài.

## Kích hoạt Webhook
Bạn cần bật tính năng này trong tệp `moltbot.json`:

```json5
{
  hooks: {
    enabled: true,
    token: "ma-bi-mat-cua-ban",
    path: "/hooks" // Mặc định là /hooks
  }
}
```

## Xác thực
Mọi yêu cầu gửi đến Webhook phải kèm theo mã Token. Cách khuyên dùng là gửi qua Header:
`Authorization: Bearer <ma-token>`

## Các địa chỉ (Endpoints) chính

### 1. Đánh thức Bot (`POST /hooks/wake`)
Dùng để thông báo một sự kiện vừa xảy ra nhưng không yêu cầu Agent phải trả lời ngay lập tức (nó sẽ xuất hiện ở lượt Heartbeat tiếp theo).
- **Tham số**: `text` (nội dung sự kiện), `mode` (`now` hoặc `next-heartbeat`).

### 2. Chạy Agent cô lập (`POST /hooks/agent`)
Dùng khi bạn muốn Bot thực hiện một hành động cụ thể và trả lời ngay.
- **Tham số**: `message` (câu lệnh cho Bot), `name` (tên nguồn gửi, VD: "GitHub"), `deliver` (có gửi kết quả về chat không).

## Ví dụ sử dụng với `curl`
```bash
curl -X POST http://127.0.0.1:18789/hooks/wake \
  -H 'Authorization: Bearer MA_BI_MAT' \
  -H 'Content-Type: application/json' \
  -d '{"text":"Cảnh báo: Máy chủ đang quá tải","mode":"now"}'
```

## Bảo mật
- Luôn giữ địa chỉ Webhook trong mạng nội bộ hoặc dùng **Tailscale** để bảo vệ.
- Sử dụng mã Token riêng biệt cho Webhook, không dùng chung mã với Gateway chính.
- Mặc định các nội dung từ Webhook được coi là không tin tưởng và sẽ được Bot xử lý một cách cẩn trọng.

---
Tài liệu liên quan: [Tích hợp Gmail Pub/Sub](./gmail-pubsub.vi.md), [Cấu hình Gateway](../gateway/configuration.vi.md).
