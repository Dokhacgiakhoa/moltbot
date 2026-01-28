---
summary: "Chạy Moltbot Gateway 24/7 trên VPS Hetzner giá rẻ dùng Docker"
read_when:
  - Bạn muốn Bot luôn online 24/7 trên máy chủ đám mây của riêng bạn
  - Bạn muốn kiểm soát hoàn toàn việc lưu trữ dữ liệu và bảo mật
---

# Moltbot trên Hetzner (Docker)

Nếu bạn muốn có một Bot Moltbot chạy **24/7 với chi phí chỉ khoảng $5 mỗi tháng**, thì Hetzner là lựa chọn đáng tin cậy và đơn giản nhất.

## Quy trình thực hiện (Dành cho người mới)

1. **Thuê máy chủ**: Thuê một gói VPS nhỏ chạy Ubuntu tại Hetzner.
2. **Cài đặt Docker**: Cài đặt môi trường chạy container để cô lập ứng dụng.
3. **Cài đặt Moltbot**: Tải mã nguồn Moltbot về máy chủ.
4. **Lưu trữ bền vững**: Gắn thư mục `~/.clawdbot` vào máy chủ để dữ liệu không bị mất khi cập nhật Bot.
5. **Truy cập bảo mật**: Sử dụng đường truyền SSH từ máy tính xách tay của bạn để điều khiển bảng điều khiển (Control UI).

## Các bước cài đặt nhanh

Trong Terminal của máy chủ Hetzner:

```bash
# 1. Cài đặt Docker
curl -fsSL https://get.docker.com | sh

# 2. Tải Moltbot
git clone https://github.com/moltbot/moltbot.git
cd moltbot

# 3. Tạo thư mục lưu trữ dữ liệu
mkdir -p /root/.clawdbot && chown -R 1000:1000 /root/.clawdbot

# 4. Khởi chạy với Docker Compose
docker compose up -d
```

## Lưu ý về Bảo mật
- **Không mở cửa tự do**: Mặc định chúng tôi khuyên bạn chỉ cho phép truy cập bảng điều khiển từ localhost (`127.0.0.1`) và kết nối thông qua **SSH Tunnel** từ máy tính của bạn.
- **Mã Token**: Hãy luôn sử dụng `CLAWDBOT_GATEWAY_TOKEN` mạnh để bảo vệ quyền truy cập.

## Truy cập bảng điều khiển từ máy tính của bạn
Chạy lệnh này trên máy tính cá nhân để "bắc cầu" kết nối tới máy chủ Hetzner:
```bash
ssh -N -L 18789:127.0.0.1:18789 root@IP_MAY_CHU_CUA_BAN
```
Sau đó mở trình duyệt và truy cập `http://127.0.0.1:18789`.

---
Tài liệu liên quan: [Hướng dẫn Docker](../../install/docker.vi.md), [Xử lý lỗi](../gateway/troubleshooting.vi.md).
