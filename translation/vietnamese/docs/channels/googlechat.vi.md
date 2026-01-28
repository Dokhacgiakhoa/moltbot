---
summary: "Trạng thái hỗ trợ, khả năng và cấu hình cho ứng dụng Google Chat"
read_when:
  - Bạn đang thiết lập kênh Google Chat qua webhook
---
# Google Chat (Chat API)

Trạng thái: Hỗ trợ tin nhắn trực tiếp (DM) và các Không gian làm việc (Spaces) thông qua webhooks của Google Chat API (chỉ hỗ trợ giao thức HTTP).

## Thiết lập nhanh (cho người mới)
1) Tạo một dự án trên Google Cloud và bật **Google Chat API**.
2) Tạo một **Service Account** (Tài khoản dịch vụ) và tải file **JSON Key** về máy.
3) Lưu file JSON này vào máy chủ chạy Gateway (ví dụ: `~/.clawdbot/googlechat-service-account.json`).
4) Trên trang cấu hình Google Chat API:
   - Thiết lập loại kết nối là **HTTP endpoint URL**.
   - Nhập URL công khai của Gateway (ví dụ: `https://domain.com/googlechat`).
   - Bật các tính năng tương tác và cho phép bot tham gia các Không gian làm việc.
5) Cấu hình Moltbot trỏ tới file JSON của Service Account và URL webhook tương ứng.
6) Chạy Gateway. Google Chat sẽ gửi dữ liệu (POST) tới đường dẫn webhook bạn đã cấu hình.

## Yêu cầu về URL công khai
Vì Google Chat sử dụng Webhook để gửi tin nhắn cho bot, bạn cần một địa chỉ HTTPS công khai.
- **Tailscale Funnel (Khuyên dùng)**: Cách an toàn nhất để chỉ lộ đường dẫn `/googlechat` ra internet mà vẫn giữ các phần khác của dashboard ở chế độ riêng tư.
- **Reverse Proxy (như Caddy)**: Chỉ chuyển hướng các yêu cầu đến `/googlechat` vào Moltbot.

## Cách thức hoạt động
- **Xác thực**: Moltbot sẽ kiểm tra mã thông báo Bearer trong tiêu đề tin nhắn từ Google để đảm bảo tính xác thực.
- **Phiên làm việc**:
  - DM sử dụng khóa phiên dựa trên `spaceId`.
  - Không gian làm việc (Spaces) yêu cầu nhắc tên (@mentions) theo mặc định.
- **Ghép nối**: Lần đầu tiên nhắn tin trực tiếp, bot sẽ yêu cầu mã ghép nối để bảo mật.

## Cấu hình mẫu
```json5
{
  channels: {
    "googlechat": {
      enabled: true,
      serviceAccountFile: "/đường/dẫn/đến/file-key.json",
      audience: "https://gateway.example.com/googlechat",
      dm: {
        policy: "pairing",
        allowFrom: ["name@example.com"]
      }
    }
  }
}
```

---
Tài liệu liên quan: [Cấu hình Gateway](../../gateway/configuration.vi.md), [Bảo mật](../../gateway/security/index.vi.md).
