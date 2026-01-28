---
summary: "Tích hợp WhatsApp (kết nối web): đăng nhập, hộp thư, phản hồi, media và vận hành"
read_when:
  - Bạn đang làm việc với hành vi của kênh WhatsApp hoặc điều hướng tin nhắn
---
# WhatsApp (kết nối web)

Trạng thái: Sử dụng WhatsApp Web thông qua thư viện Baileys. Gateway sở hữu các phiên làm việc.

## Thiết lập nhanh (Dành cho người mới)
1) Sử dụng một **số điện thoại riêng biệt** nếu có thể (khuyên dùng).
2) Cấu hình WhatsApp trong file `~/.clawdbot/moltbot.json`.
3) Chạy lệnh `moltbot channels login` để quét mã QR (Thiết bị đã liên kết).
4) Khởi động gateway.

Cấu hình tối thiểu:
```json5
{
  channels: {
    whatsapp: {
      dmPolicy: "allowlist",
      allowFrom: ["+84..."] // Số điện thoại của bạn (người chủ)
    }
  }
}
```

## Chọn số điện thoại (Hai chế độ)

WhatsApp yêu cầu một số điện thoại di động thực để xác minh.

### Số riêng biệt (Khuyên dùng)
Sử dụng một **số điện thoại riêng** cho Moltbot. Đây là cách thiết lập tốt nhất, giúp điều hướng tin nhắn sạch sẽ và không gặp lỗi tin nhắn tự gửi cho chính mình. Thiết lập lý tưởng: **điện thoại Android cũ/giá rẻ + eSIM/SIM trả trước**. Cắm sạc và bật Wi-Fi 24/7, sau đó liên kết qua mã QR.

Bạn có thể dùng **WhatsApp Business** trên cùng một thiết bị với một số khác để tách biệt với WhatsApp cá nhân.

### Số cá nhân (Phương án dự phòng)
Chạy Moltbot trên **chính số điện thoại của bạn**. Bạn có thể nhắn tin cho chính mình (mục "Nhắn tin cho chính mình" trên WhatsApp) để thử nghiệm. **Bắt buộc phải bật chế độ self-chat.**

Cấu hình mẫu (số cá nhân, self-chat):
```json5
{
  channels: {
    whatsapp: {
      selfChatMode: true,
      dmPolicy: "allowlist",
      allowFrom: ["+84..."]
    }
  }
}
```

## Đăng nhập & Thông tin xác thực
- Lệnh đăng nhập: `moltbot channels login` (Quét QR qua Thiết bị đã liên kết).
- Hỗ trợ nhiều tài khoản: `moltbot channels login --account <id>`.
- Thông tin xác thực được lưu tại `~/.clawdbot/credentials/whatsapp/<accountId>/creds.json`.
- Đăng xuất: `moltbot channels logout` sẽ xóa trạng thái xác thực WhatsApp.

## Quy trình tin nhắn đến (DM + Nhóm)
- **Chính sách DM**: `channels.whatsapp.dmPolicy` kiểm soát quyền truy cập chat trực tiếp (mặc định: `pairing`).
  - `pairing`: người lạ nhắn tin sẽ nhận được mã ghép đôi (phê duyệt qua lệnh `moltbot pairing approve whatsapp <code>`).
  - `allowlist`: chỉ những số trong danh sách `allowFrom` mới được phép chat.
- Tin nhắn tự gửi cho chính mình luôn được phép; nhưng "chế độ self-chat" vẫn yêu cầu số của bạn phải nằm trong `allowFrom`.

## Thông báo đã đọc (Dấu tích xanh)
Mặc định, gateway sẽ đánh dấu các tin nhắn WhatsApp đã đọc (tích xanh) ngay khi chúng được tiếp nhận.

Tắt tính năng này:
```json5
{
  channels: { whatsapp: { sendReadReceipts: false } }
}
```

## Nhóm chat (Groups)
- Nhóm được ánh xạ tới phiên: `agent:<agentId>:whatsapp:group:<jid>`.
- Chế độ kích hoạt:
  - `mention` (mặc định): yêu cầu phải @mention bot hoặc khớp regex.
  - `always`: luôn phản hồi mọi tin nhắn trong nhóm.
- Gửi lệnh `/activation always` hoặc `/activation mention` ngay trong nhóm để thay đổi chế độ (chỉ dành cho chủ sở hữu).

## Phản hồi nhanh (Acknowledge reactions)
WhatsApp có thể tự động gửi cảm xúc (emoji) cho tin nhắn ngay khi nhận được, trước khi bot tạo phản hồi. Cách này báo cho người dùng biết bot đã nhận được tin nhắn.

Cấu hình:
```json5
{
  channels: {
    whatsapp: {
      ackReaction: {
        emoji: "👀",
        direct: true,
        group: "mentions"
      }
    }
  }
}
```

---
Tài liệu liên quan: [Bảo mật](../gateway/security.vi.md), [Ghép nối](../start/pairing.vi.md).
