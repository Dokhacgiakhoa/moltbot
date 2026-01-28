---
summary: "Chạy cầu nối ACP để tích hợp với các môi trường lập trình (IDE)"
read_when:
  - Bạn muốn thiết lập tích hợp Moltbot với các IDE (như Zed, VS Code)
  - Bạn cần sửa lỗi điều phối phiên làm việc thông qua Gateway
---

# acp (Agent Client Protocol)

Lệnh này khởi chạy cầu nối ACP giúp giao tiếp giữa các IDE (môi trường lập trình) và Moltbot Gateway.

Cầu nối này nhận các yêu cầu ACP qua luồng vào/ra chuẩn (stdio) và chuyển tiếp chúng tới Gateway thông qua WebSocket, giúp giữ cho các phiên làm việc trong IDE luôn đồng bộ với Agent.

## Cách sử dụng

```bash
# Chạy cầu nối ACP cục bộ
moltbot acp

# Kết nối tới Gateway từ xa
moltbot acp --url wss://di-chi-gateway:18789 --token <mã-token>

# Gắn vào một phiên làm việc cụ thể
moltbot acp --session agent:main:main
```

## Cách thiết lập với trình soạn thảo Zed
Thêm phần cấu hình sau vào file `~/.config/zed/settings.json`:

```json
{
  "agent_servers": {
    "Moltbot ACP": {
      "type": "custom",
      "command": "moltbot",
      "args": ["acp"],
      "env": {}
    }
  }
}
```

Sau khi cấu hình, bạn có thể mở bảng Agent trong Zed và chọn "Moltbot ACP" để bắt đầu trò chuyện với bot ngay trong môi trường code.

## Quản lý phiên làm việc
Mặc định, các phiên ACP sẽ có tên bắt đầu bằng tiền tố `acp:`. Bạn có thể sử dụng cờ `--reset-session` để tạo một phiên trò chuyện mới hoàn toàn (nhưng vẫn giữ nguyên các cài đặt cấu hình).

---
Tài liệu liên quan: [Khái niệm phiên làm việc](../../concepts/session.vi.md), [Cấu hình Gateway](../gateway/configuration.vi.md).
