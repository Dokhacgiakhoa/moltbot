---
summary: "Cài đặt Moltbot tự động và bảo mật bằng Ansible, Tailscale VPN và cô lập tường lửa"
read_when:
  - Bạn muốn triển khai máy chủ tự động với các thiết lập bảo mật tối ưu
  - Bạn cần thiết lập hệ thống qua VPN và bị chặn bởi tường lửa
  - Bạn đang triển khai trên máy chủ Debian/Ubuntu từ xa
---

# Cài đặt qua Ansible

Cách khuyên dùng để triển khai Moltbot lên các máy chủ sản xuất (production) là thông qua **[moltbot-ansible](https://github.com/moltbot/moltbot-ansible)** — một trình cài đặt tự động với kiến trúc ưu tiên bảo mật.

## Bắt đầu nhanh

Cài đặt chỉ với một câu lệnh:

```bash
curl -fsSL https://raw.githubusercontent.com/moltbot/moltbot-ansible/main/install.sh | bash
```

> **📦 Hướng dẫn đầy đủ: [github.com/moltbot/moltbot-ansible](https://github.com/moltbot/moltbot-ansible)**
>
> Kho lưu trữ `moltbot-ansible` là nguồn thông tin chính thức cho việc triển khai qua Ansible. Trang này chỉ cung cấp cái nhìn tổng quan nhanh.

## Những gì bạn sẽ nhận được

- 🔒 **Bảo mật tường lửa**: Sử dụng UFW + cô lập Docker (Chỉ có thể truy cập qua SSH + Tailscale).
- 🔐 **Tailscale VPN**: Truy cập từ xa an toàn mà không cần công khai các dịch vụ ra internet.
- 🐳 **Docker**: Các container "hộp cát" cô lập cho Agent, chỉ lắng nghe ở địa chỉ localhost.
- 🛡️ **Phòng thủ đa lớp**: Kiến trúc bảo mật 4 lớp.
- 🚀 **Thiết lập một chạm**: Hoàn tất triển khai chỉ trong vài phút.
- 🔧 **Tích hợp Systemd**: Tự động chạy khi khởi động máy với các thiết lập bảo mật.

## Yêu cầu hệ thống

- **Hệ điều hành**: Debian 11+ hoặc Ubuntu 20.04+
- **Quyền hạn**: Quyền Root hoặc sudo
- **Mạng**: Kết nối internet để tải các gói cài đặt
- **Ansible**: Phiên bản 2.14+ (Sẽ được tự động cài đặt bởi kịch bản bắt đầu nhanh)

---
Tài liệu liên quan: [Cơ chế cô lập (Sandboxing)](../gateway/sandboxing.vi.md), [Cập nhật hệ thống](./updating.vi.md).
