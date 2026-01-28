---
summary: "Thiết lập đường truyền SSH (SSH tunnel) để ứng dụng Moltbot.app kết nối với Gateway từ xa"
read_when:
  - Bạn muốn sử dụng ứng dụng Moltbot trên Mac để điều khiển máy chủ Moltbot ở xa qua SSH
---

# Sử dụng Moltbot.app với Gateway từ xa

Moltbot.app trên máy Mac của bạn có thể sử dụng cơ chế SSH tunneling để kết nối đến một máy chủ Gateway đang chạy ở xa (ví dụ: trên VPS hoặc máy chủ tại nhà).

## Sơ đồ hoạt động
Kết nối từ ứng dụng Mac của bạn sẽ được "đóng gói" và gửi qua đường truyền SSH an toàn để đến được máy chủ:
`Ứng dụng Mac (Cổng 18789) -> SSH Tunnel -> Máy chủ từ xa (Cổng 18789)`

## Các bước thiết lập nhanh

### Bước 1: Cấu hình tệp SSH
Mở tệp `~/.ssh/config` trên máy Mac của bạn và thêm đoạn mã sau:

```ssh
Host remote-gateway
    HostName <DIA_CHI_IP_MAY_CHU>
    User <TEN_NGUOI_DUNG>
    LocalForward 18789 127.0.0.1:18789
    IdentityFile ~/.ssh/id_rsa
```

### Bước 2: Chép khóa SSH (Nếu cần)
Để việc kết nối không cần nhập mật khẩu mỗi lần, hãy chép khóa công khai của bạn lên máy chủ:
```bash
ssh-copy-id -i ~/.ssh/id_rsa <TEN_NGUOI_DUNG>@<DIA_CHI_IP_MAY_CHU>
```

### Bước 3: Khởi động đường truyền SSH
Dùng lệnh sau trong Terminal để mở đường truyền:
```bash
ssh -N remote-gateway &
```

### Bước 4: Khởi động lại ứng dụng Moltbot
Tắt hẳn Moltbot.app (⌘Q) rồi mở lại. Bây giờ ứng dụng sẽ tự động kết nối đến máy chủ từ xa của bạn.

## Tự động khởi động đường truyền khi đăng nhập (Dành cho chuyên gia)
Bạn có thể tạo một tệp `plist` trong thư mục `~/Library/LaunchAgents/` để macOS tự động mở đường truyền SSH mỗi khi bạn mở máy tính.

**Tên tệp**: `bot.molt.ssh-tunnel.plist`
**Nội dung**: Sử dụng chương trình `/usr/bin/ssh` với các tham số `-N remote-gateway`.

Sau khi tạo tệp, hãy nạp nó vào hệ thống bằng lệnh:
```bash
launchctl bootstrap gui/$UID ~/Library/LaunchAgents/bot.molt.ssh-tunnel.plist
```

## Cách kiểm tra đường truyền đã hoạt động chưa
Gõ lệnh sau vào Terminal:
```bash
lsof -i :18789
```
Nếu bạn thấy có tiến trình `ssh` đang lắng nghe ở cổng này, nghĩa là đường truyền đã sẵn sàng.

---
Tài liệu liên quan: [Truy cập từ xa](./remote.vi.md), [Bảo mật](./security/index.vi.md).
