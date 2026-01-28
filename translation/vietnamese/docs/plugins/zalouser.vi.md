---
summary: "Plugin Zalo Cá nhân: Đăng nhập bằng mã QR và nhắn tin qua zca-cli"
read_when:
  - Bạn muốn Moltbot hỗ trợ nhắn tin qua tài khoản Zalo cá nhân của mình
---

# Zalo Cá nhân (Plugin)

Moltbot hỗ trợ tích hợp với tài khoản Zalo cá nhân thông qua plugin `zalouser`. Plugin này sử dụng công cụ `zca-cli` để tự động hóa các thao tác trên tài khoản Zalo của bạn.

> **Cảnh báo:** Việc sử dụng các công cụ tự động hóa không chính thức có thể dẫn đến việc tài khoản Zalo bị khóa hoặc tạm ngưng. Hãy cân nhắc kỹ và tự chịu trách nhiệm khi sử dụng.

## Cơ chế hoạt động
Plugin này chạy trực tiếp bên trong tiến trình Gateway. Khi bạn đăng nhập, một mã QR sẽ hiển thị để bạn dùng ứng dụng Zalo trên điện thoại quét và cấp quyền.

## Cài đặt
1) Cài đặt plugin:
   ```bash
   moltbot plugins install @moltbot/zalouser
   ```
2) Đảm bảo máy chủ của bạn đã cài đặt công cụ `zca`:
   ```bash
   zca --version
   ```
3) Khởi động lại Gateway.

## Cấu hình
Bạn cần bật kênh Zalo trong phần `channels` của tệp cài đặt:
```json5
{
  "channels": {
    "zalouser": {
      "enabled": true
    }
  }
}
```

## Các lệnh điều khiển (CLI)
- `moltbot channels login --channel zalouser`: Hiển thị mã QR để đăng nhập.
- `moltbot message send --channel zalouser --target <id_nguoi_nhan> --message "Chào bạn"`: Gửi tin nhắn.

## Khả năng của Bot
Khi được kích hoạt, Bot có thể:
- Gửi tin nhắn văn bản, hình ảnh, đường dẫn.
- Xem danh sách bạn bè và các nhóm chat.
- Tự động phản hồi các tin nhắn đến.

---
Tài liệu liên quan: [Kênh nhắn tin](../../channels/index.vi.md), [Cài đặt Plugin](./index.vi.md).
