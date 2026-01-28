---
summary: "Hỗ trợ Linux + Tình trạng ứng dụng đi kèm"
read_when:
  - Bạn đang tìm hiểu về cài đặt Moltbot trên Linux
  - Bạn muốn thiết lập Gateway chạy như một dịch vụ hệ thống (systemd)
---

# Chạy Moltbot trên Linux

Gateway Moltbot được hỗ trợ đầy đủ trên Linux. **Node.js là môi trường chạy được khuyên dùng**.

## Cách cài đặt nhanh (Dành cho máy chủ VPS)

1. Cài đặt Node 22+.
2. Cài đặt Moltbot: `npm i -g moltbot@latest`.
3. Chạy trình hướng dẫn: `moltbot onboard --install-daemon`.
4. Thiết lập đường truyền an toàn từ máy cá nhân: `ssh -N -L 18789:127.0.0.1:18789 <user>@<ip-may-chu>`.
5. Mở địa chỉ `http://127.0.0.1:18789/` trên trình duyệt và dán mã Token vào.

## Quản lý dịch vụ với Systemd
Moltbot mặc định cài đặt dịch vụ dưới dạng **user service** của systemd.

Để kiểm tra trạng thái dịch vụ:
```bash
systemctl --user status moltbot-gateway.service
```

Để xem nhật ký hoạt động:
```bash
journalctl --user -u moltbot-gateway.service -f
```

## Các phương thức cài đặt khác
- [Cài đặt với Nix](../../install/nix.vi.md)
- [Cài đặt với Docker](../../install/docker.vi.md)
- [Sử dụng Bun (Thử nghiệm)](../../install/bun.vi.md)

---
Tài liệu liên quan: [Bắt đầu nhanh](../../start/getting-started.vi.md), [Cấu hình Gateway](../../gateway/configuration.vi.md).
