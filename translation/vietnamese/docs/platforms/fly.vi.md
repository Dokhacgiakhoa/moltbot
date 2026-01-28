---
title: Fly.io
summary: "Hướng dẫn triển khai Moltbot trên nền tảng Fly.io với bộ nhớ lưu trữ vĩnh viễn"
read_when:
  - Bạn muốn chạy Bot 24/7 trên đám mây với chi phí thấp (có gói miễn phí)
---

# Triển khai trên Fly.io

**Mục tiêu:** Chạy Moltbot Gateway trên một máy chủ [Fly.io](https://fly.io) với ổ cứng lưu trữ bền vững, tự động cấu hình HTTPS và có khả năng truy cập qua Discord/Telegram.

## Các bước chuẩn bị
- Đã cài đặt công cụ [flyctl CLI](https://fly.io/docs/hands-on/install-flyctl/).
- Tài khoản Fly.io (Gói miễn phí là đủ dùng).
- Khóa API của nhà cung cấp AI (Anthropic, OpenAI, v.v.).

## Lộ trình thực hiện nhanh

1. **Tạo ứng dụng Fly**:
   ```bash
   git clone https://github.com/moltbot/moltbot.git
   cd moltbot
   fly apps create ten-ứng-dụng-của-bạn
   ```

2. **Tạo ổ cứng lưu trữ (Volume)**:
   ```bash
   fly volumes create moltbot_data --size 1 --region iad
   ```

3. **Thiết lập bí mật (Secrets)**:
   ```bash
   # Bắt buộc: Mã xác thực Gateway
   fly secrets set CLAWDBOT_GATEWAY_TOKEN=$(openssl rand -hex 32)
   # Khóa API AI
   fly secrets set ANTHROPIC_API_KEY=sk-ant-...
   ```

4. **Triển khai**:
   ```bash
   fly deploy
   ```

## Các cấu hình quan trọng trong `fly.toml`

Để Bot hoạt động ổn định trên Fly.io, bạn cần lưu ý:
- **Bộ nhớ (RAM)**: Fly mặc định cấp 512MB, nhưng mức này thường gây lỗi tràn bộ nhớ (OOM). Hãy nâng lên ít nhất **1GB (1024mb)** hoặc tốt nhất là **2GB**.
- **Địa chỉ IP**: Webhook của Moltbot cần IP để nhận tin nhắn. Bạn có thể chọn triển khai công khai (Public) hoặc riêng tư (Private) qua mạng WireGuard/Tailscale.
- **Lưu trữ trạng thái**: Đảm bảo biến `CLAWDBOT_STATE_DIR` trỏ tới thư mục `/data` (nơi gắn ổ cứng đã tạo ở bước 2).

## Xử lý sự cố thường gặp
- **Lỗi Gateway Lock**: Nếu công nương (container) bị khởi động lại đột ngột, tệp khóa có thể còn sót lại trên ổ cứng. Hãy dùng `fly ssh console` để xóa tệp `/data/gateway.*.lock`.
- **Lỗi bộ nhớ**: Nếu Bot liên tục bị sập và khởi động lại, hãy nâng cấp RAM của máy ảo Fly bằng lệnh: `fly machine update <id> --vm-memory 2048`.

---
Tài liệu liên quan: [Thuê máy chủ VPS](../../vps.vi.md), [Cấu hình Gateway](../../gateway/configuration.vi.md).
