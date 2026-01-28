---
summary: "Hỗ trợ Windows (WSL2) + Tình trạng ứng dụng đi kèm"
read_when:
  - Bạn muốn cài đặt Moltbot trên máy tính chạy Windows
  - Bạn đang tìm hiểu về cách sử dụng cổng chuyển tiếp portproxy trong WSL2
---

# Moltbot trên Windows (WSL2)

Cách khuyên dùng để chạy Moltbot trên Windows là thông qua **WSL2** (khuyên dùng Ubuntu). Việc chạy bên trong môi trường Linux giúp hệ thống hoạt động ổn định nhất, tương thích tốt với các công cụ phát triển (Node/pnpm) và các kỹ năng của Agent.

## Cài đặt (WSL2)

### 1) Cài đặt WSL2 + Ubuntu
Mở PowerShell với quyền Quản trị (Admin) và chạy:
```powershell
wsl --install -d Ubuntu-24.04
```
Khởi động lại máy nếu Windows yêu cầu.

### 2) Kích hoạt systemd
Để cài đặt dịch vụ Gateway, bạn cần bật systemd bên trong WSL. Trong cửa sổ Ubuntu, chạy lệnh:
```bash
sudo tee /etc/wsl.conf >/dev/null <<'EOF'
[boot]
systemd=true
EOF
```
Sau đó khởi động lại WSL từ PowerShell: `wsl --shutdown`.

### 3) Cài đặt Moltbot
Tiến hành cài đặt như trên Linux bình thường bên trong cửa sổ Ubuntu:
```bash
npm install -g moltbot@latest
moltbot onboard --install-daemon
```

## Nâng cao: Truy cập Gateway từ mạng nội bộ
Mặc định WSL sử dụng một lớp mạng ảo riêng. Nếu bạn muốn các thiết bị khác (như điện thoại) có thể kết nối vào Gateway đang chạy trong WSL, bạn cần thực hiện chuyển tiếp cổng bằng lệnh `netsh` trên Windows.

**Mẹo**: Hãy sử dụng lệnh `moltbot status --all` để kiểm tra địa chỉ IP nào các thiết bị khác có thể nhìn thấy.

---
Tài liệu liên quan: [Bắt đầu nhanh](../../start/getting-started.vi.md), [Hướng dẫn Linux](./linux.vi.md).
