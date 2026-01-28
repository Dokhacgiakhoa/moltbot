---
summary: "Hướng dẫn cài đặt Moltbot trên DigitalOcean (VPS trả phí đơn giản nhất)"
read_when:
  - Bạn cần một máy chủ ổn định với quy trình cài đặt cực kỳ nhanh gọn
  - Bạn muốn sử dụng giao diện web trực quan của DigitalOcean
---

# Moltbot trên DigitalOcean

DigitalOcean là lựa chọn tuyệt vời cho những ai muốn sự đơn giản. Với khoảng **$6/tháng**, bạn có một máy chủ (Droplet) chạy Moltbot Gateway ổn định.

## Các bước thực hiện

1. **Tạo Droplet**:
   - Chọn khu vực gần bạn nhất (ví dụ: Singapore nếu bạn ở Việt Nam).
   - Chọn hình ảnh: Ubuntu 24.04 LTS.
   - Chọn cấu hình: Basic -> Regular với mức giá $6/tháng.
2. **Cài đặt**: Kết nối qua SSH và chạy kịch bản cài đặt:
   ```bash
   curl -fsSL https://molt.bot/install.sh | bash
   moltbot onboard --install-daemon
   ```
3. **Truy cập**: Sử dụng SSH Tunnel để vào bảng điều khiển:
   ```bash
   ssh -L 18789:localhost:18789 root@IP_CUA_BAN
   ```

## Tối ưu bộ nhớ (Dành cho gói 1GB RAM)
Máy chủ $6 thường chỉ có 1GB RAM, đôi khi Agent sẽ gặp lỗi tràn bộ nhớ. Bạn nên tạo thêm tệp SWAP (bộ nhớ ảo) để máy chạy mượt hơn:
```bash
# Tạo 2GB bộ nhớ ảo
fallocate -l 2G /swapfile
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
```

---
Tài liệu liên quan: [Hướng dẫn Hetzner](./hetzner.vi.md) (Rẻ hơn và mạnh hơn), [Bắt đầu nhanh](../../start/getting-started.vi.md).
