---
summary: "Hỗ trợ iMessage qua công cụ imsg (JSON-RPC qua stdio), thiết lập và điều hướng tin nhắn"
read_when:
  - Thiết lập hỗ trợ iMessage trên macOS
---
# iMessage (imsg)

Trạng thái: Tích hợp qua công cụ CLI bên ngoài. Gateway chạy lệnh `imsg rpc` (giao thức JSON-RPC qua đầu vào/đầu ra tiêu chuẩn).

## Thiết lập nhanh (cho người mới)
1) Đảm bảo ứng dụng **Messages** đã đăng nhập Apple ID trên máy Mac này.
2) Cài đặt công cụ `imsg`: `brew install steipete/tap/imsg`.
3) Cấu hình Moltbot với đường dẫn đến CLI `imsg` và file cơ sở dữ liệu `chat.db`.
4) Chạy Gateway và phê duyệt các yêu cầu cấp quyền từ macOS (Tự động hóa + Quyền truy cập toàn bộ đĩa).

## Đặc điểm nổi bật
- **Chạy trên macOS**: Đây là kênh giao tiếp dành riêng cho hệ sinh thái Apple.
- **Điều hướng ổn định**: Câu trả lời của bot sẽ luôn quay lại đúng cuộc trò chuyện iMessage tương ứng.
- **Tách biệt danh tính**: Bạn có thể thiết lập một người dùng macOS riêng biệt để bot hoạt động với một Apple ID độc lập, giữ cho tin nhắn cá nhân của bạn không bị lẫn lộn.

## Yêu cầu hệ thống
- Máy Mac luôn bật và đã đăng nhập iMessage.
- Quyền **Full Disk Access** (Truy cập toàn bộ đĩa) cho Moltbot và `imsg` để đọc cơ sở dữ liệu tin nhắn.
- Quyền **Automation** để bot có thể gửi tin nhắn thay mặt bạn.

## Cấu hình mẫu
```json5
{
  channels: {
    imessage: {
      enabled: true,
      cliPath: "/usr/local/bin/imsg",
      dbPath: "/Users/Tên_Người_Dùng/Library/Messages/chat.db"
    }
  }
}
```

## Chế độ từ xa (SSH)
Nếu bạn chạy Gateway trên Linux nhưng muốn dùng iMessage trên máy Mac, bạn có thể thiết lập để Gateway kết nối tới máy Mac qua SSH và chạy lệnh `imsg` từ xa. Moltbot hỗ trợ tự động tải về các tệp đính kèm qua giao thức SCP trong chế độ này.

---
Tài liệu liên quan: [Ghép nối thiết bị](../../start/pairing.vi.md), [Cấu hình Gateway](../../gateway/configuration.vi.md).
