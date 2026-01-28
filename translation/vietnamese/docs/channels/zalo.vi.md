---
summary: "Trạng thái hỗ trợ Zalo bot, các khả năng và cấu hình"
read_when:
  - Đang làm việc với các tính năng Zalo hoặc webhook
---
# Zalo (Bot API)

Trạng thái: Đang thử nghiệm (experimental). Hiện tại chỉ hỗ trợ tin nhắn trực tiếp (DM); nhóm chat đang được phát triển theo lộ trình của Zalo.

## Yêu cầu Plugin
Zalo được cung cấp dưới dạng plugin và không đi kèm sẵn trong bản cài đặt cốt lõi.
- Cài đặt qua CLI: `moltbot plugins install @moltbot/zalo`
- Chi tiết: [Plugins](../plugin.vi.md)

## Thiết lập nhanh (Dành cho người mới)
1) Cài đặt plugin Zalo.
2) Thiết lập mã token:
   - Biến môi trường: `ZALO_BOT_TOKEN=...`
   - Hoặc cấu hình: `channels.zalo.botToken: "..."`.
3) Khởi động lại gateway.
4) Quyền truy cập DM mặc định là `pairing` (ghép đôi); hãy phê duyệt mã ghép đôi trong lần liên lạc đầu tiên.

Cấu hình tối thiểu:
```json5
{
  channels: {
    zalo: {
      enabled: true,
      botToken: "12345689:abc-xyz",
      dmPolicy: "pairing"
    }
  }
}
```

## Tổng quan
Zalo là ứng dụng nhắn tin phổ biến nhất tại Việt Nam. Bot API cho phép Gateway chạy một con bot để hội thoại 1:1.
- Một kênh Zalo Bot API do Gateway sở hữu.
- Định tuyến xác định: phản hồi sẽ quay lại Zalo.
- DM chia sẻ phiên làm việc chính của agent.
- Nhóm chat chưa được hỗ trợ (tài liệu Zalo ghi "sắp ra mắt").

## Thiết lập (Các bước nhanh)

### 1) Tạo bot token (Zalo Bot Platform)
1) Truy cập **https://bot.zaloplatforms.com** và đăng nhập.
2) Tạo một bot mới và cấu hình các cài đặt.
3) Sao chép bot token (định dạng: `12345689:abc-xyz`).

## Cách hoạt động
- Tin nhắn đến được chuẩn hóa vào khung chung của kênh kèm theo các vị trí chờ cho media.
- Phản hồi luôn quay lại đúng cuộc chat Zalo đó.
- Sử dụng long-polling mặc định; chế độ webhook có sẵn qua `channels.zalo.webhookUrl`.

## Giới hạn
- Văn bản gửi đi được chia nhỏ mỗi 2000 ký tự (giới hạn của Zalo API).
- Truyền phát dữ liệu (Streaming) bị chặn theo mặc định do giới hạn 2000 ký tự làm cho tính năng này kém hiệu quả.

## Kiểm soát quyền truy cập (DM)
- Mặc định: `channels.zalo.dmPolicy = "pairing"`. Người lạ nhắn tin sẽ nhận được mã ghép đôi; tin nhắn bị bỏ qua cho đến khi được phê duyệt (mã hết hạn sau 1 giờ).
- Phê duyệt qua lệnh:
  - `moltbot pairing list zalo`
  - `moltbot pairing approve zalo <MÃ_CODE>`
- `channels.zalo.allowFrom` chấp nhận các ID người dùng dạng số.

---
Tài liệu liên quan: [Plugins](../plugin.vi.md), [Ghép nối](../start/pairing.vi.md).
