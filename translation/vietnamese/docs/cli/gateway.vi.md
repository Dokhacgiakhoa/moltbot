---
summary: "Tài liệu tham khảo lệnh `moltbot gateway` — khởi chạy, truy vấn và tìm kiếm gateway"
read_when:
  - Bạn muốn chạy Gateway từ dòng lệnh
  - Bạn cần kiểm tra kết nối và xác thực của Gateway
---

# Lệnh Gateway

Gateway là máy chủ WebSocket trung tâm của Moltbot, chịu trách nhiệm quản lý các kênh chat, agent, phiên làm việc và các công cụ khác.

Tài liệu liên quan:
- [Bonjour (Khám phá mạng)](../gateway/bonjour.vi.md)
- [Cấu hình hệ thống](../gateway/configuration.vi.md)

## Khởi chạy Gateway

Chạy một Gateway cục bộ:
```bash
moltbot gateway
```

Chạy trực tiếp (không chạy ngầm):
```bash
moltbot gateway run
```

**Lưu ý quan trọng**: 
- Mặc định Gateway sẽ không chạy nếu cấu hình `gateway.mode` chưa được đặt là `local`. Bạn có thể dùng cờ `--allow-unconfigured` để chạy thử nghiệm.
- Việc kết nối từ bên ngoài (LAN/Internet) mà không có mật khẩu/token sẽ bị chặn để đảm bảo an toàn.

## Tùy chọn khởi chạy (Options)
- `--port <cổng>`: Cổng WebSocket (mặc định là `18789`).
- `--bind <loopback|lan|tailnet|auto|custom>`: Chế độ liên kết địa chỉ mạng.
- `--token <token>` / `--password <mật khẩu>`: Đè lên cấu hình xác thực hiện có.
- `--tailscale <off|serve|funnel>`: Công khai Gateway qua mạng Tailscale.
- `--force`: Buộc đóng bất kỳ ứng dụng nào đang chiếm dụng cổng trước khi chạy.
- `--verbose`: Hiển thị nhật ký chi tiết.

## Truy vấn Gateway đang chạy

Bạn có thể sử dụng các lệnh sau để kiểm tra trạng thái của một Gateway đang hoạt động (cục bộ hoặc từ xa):

### `gateway health`
Kiểm tra sức khỏe cơ bản của Gateway.
```bash
moltbot gateway health --url ws://127.0.0.1:18789
```

### `gateway status`
Xem trạng thái dịch vụ hệ thống (launchd/systemd) và thăm dò RPC.
```bash
moltbot gateway status
```

### `gateway probe`
Lệnh chẩn đoán "tất cả trong một". Nó sẽ kiểm tra cả Gateway cục bộ và Gateway từ xa (nếu có cấu hình).

## Quản lý dịch vụ Gateway
Nếu bạn cài đặt Moltbot như một dịch vụ hệ thống, hãy dùng các lệnh sau:
```bash
moltbot gateway install   # Cài đặt dịch vụ
moltbot gateway start     # Khởi động dịch vụ
moltbot gateway stop      # Dừng dịch vụ
moltbot gateway restart   # Khởi động lại
moltbot gateway uninstall # Gỡ bỏ dịch vụ
```

## Tìm kiếm Gateway trong mạng nội bộ (Bonjour)
Moltbot hỗ trợ tự động tìm kiếm các bộ Gateway khác đang chạy trong cùng mạng Wi-Fi hoặc mạng Tailscale.
```bash
moltbot gateway discover
```

---
Tài liệu liên quan: [Cổng kết nối từ xa](../gateway/remote.vi.md), [Bảo mật](../gateway/security/index.vi.md).
