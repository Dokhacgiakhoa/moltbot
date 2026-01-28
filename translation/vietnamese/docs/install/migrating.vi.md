---
summary: "Di chuyển (migrate) cài đặt Moltbot từ máy tính này sang máy tính khác"
read_when:
  - Bạn vừa mua máy tính mới hoặc muốn chuyển Bot lên máy chủ
  - Bạn muốn giữ nguyên các phiên chat, khóa API và trạng thái đăng nhập WhatsApp/Telegram
---

# Di chuyển Moltbot sang máy mới

Hướng dẫn này giúp bạn di chuyển Gateway Moltbot sang máy tính khác mà **không cần phải thực hiện lại quy trình thiết lập (onboarding)** từ đầu.

Về cơ bản, việc di chuyển bao gồm hai phần chính:
1. Sao chép **Thư mục trạng thái (State directory)**: Mặc định là `~/.clawdbot/` — nơi lưu cấu hình, khóa API, các phiên chat và trạng thái kết nối các kênh.
2. Sao chép **Không gian làm việc (Workspace)**: Mặc định là `~/clawd/` — nơi lưu các tệp tin của Agent (trí nhớ, các câu lệnh nhắc, v.v.).

## Các bước thực hiện (Khuyên dùng)

### Bước 0: Sao lưu (Tại máy cũ)
Hãy dừng Gateway trước để đảm bảo dữ liệu không bị thay đổi trong quá trình chép:
```bash
moltbot gateway stop
```
Sau đó nén hai thư mục quan trọng lại:
```bash
cd ~
tar -czf moltbot-state.tgz .clawdbot
tar -czf clawd-workspace.tgz clawd
```

### Bước 1: Cài đặt Moltbot trên máy mới
Trên máy tính mới, hãy cài đặt CLI giống như cách bạn đã làm lần đầu:
- Xem: [Hướng dẫn cài đặt](./index.vi.md)

### Bước 2: Sao chép dữ liệu sang máy mới
Giải nén hai tệp tin sao lưu vào đúng vị trí tương ứng trên máy mới (thường là thư mục gốc người dùng `~`). Đảm bảo rằng:
- Các thư mục ẩn (có dấu chấm ở đầu như `.clawdbot`) đã được chép đầy đủ.
- Quyền sở hữu tệp tin thuộc về người dùng hiện tại trên máy mới.

### Bước 3: Chạy lệnh kiểm tra (Doctor)
Trên máy tính mới, hãy chạy lệnh sau để Moltbot tự động điều chỉnh các đường dẫn và dịch vụ hệ thống:
```bash
moltbot doctor
```
Sau đó khởi động lại Bot:
```bash
moltbot gateway restart
moltbot status
```

## Các lưu ý quan trọng
- **Đừng chỉ chép tệp `moltbot.json`**: Tệp này là không đủ. Bạn cần cả thư mục `credentials/` và `agents/` nằm bên trong thư mục trạng thái.
- **Quyền hạn tệp tin**: Nếu bạn chép file bằng quyền root, Bot có thể sẽ không đọc được dữ liệu. Hãy đảm bảo quyền sở hữu đúng.
- **Bảo mật**: Thư mục trạng thái chứa các khóa bí mật (API key). Hãy vận chuyển chúng qua các kênh an toàn và xóa bản sao lưu sau khi hoàn tất.

---
Tài liệu liên quan: [Lệnh Doctor](../gateway/doctor.vi.md), [Xử lý lỗi](../gateway/troubleshooting.vi.md).
