---
summary: "Truy cập từ xa bằng đường truyền SSH (Gateway WS) và mạng Tailscale"
read_when:
  - Bạn muốn sử dụng Moltbot từ xa khi không ở gần máy tính chạy Gateway
---

# Truy cập từ xa (SSH, Tunnel và Tailscale)

Moltbot hỗ trợ cơ chế "điều khiển từ xa qua SSH". Bạn có thể chạy một Gateway duy nhất (máy chủ chính) trên máy tính để bàn hoặc máy chủ dịch vụ, sau đó kết nối các ứng dụng khách từ điện thoại hoặc máy tính xách tay đến đó.

## Ý tưởng cốt lõi
- Gateway chạy trên máy chủ và lắng nghe ở địa chỉ **loopback** (thường là cổng 18789).
- Để truy cập từ xa, bạn chuyển tiếp (forward) cổng đó qua SSH hoặc sử dụng mạng ảo như VPN/Tailscale.

## Các cách thiết lập phổ biến

### 1) Gateway chạy liên tục trên VPS hoặc máy chủ tại nhà
Đây là cách tốt nhất nếu máy tính xách tay của bạn thường xuyên ở chế độ ngủ.
- **Dùng Tailscale (Khuyên dùng):** Sử dụng tính năng **Tailscale Serve** để truy cập bảng điều khiển qua HTTPS một cách an toàn nhất.
- Máy chủ sẽ giữ tất cả các phiên chat, thông tin đăng nhập và trạng thái Agent của bạn.

### 2) Máy tính nhà chạy Gateway, laptop là thiết bị điều khiển
Khi bạn đi công tác, máy tính xách tay của bạn không cần chạy Agent. Nó chỉ cần kết nối về nhà:
- Sử dụng chế độ **Remote over SSH** trong ứng dụng macOS. Ứng dụng sẽ tự động mở đường truyền (tunnel) và quản lý kết nối cho bạn.

## Dòng lệnh chuyển tiếp SSH
Nếu bạn muốn dùng Terminal để kết nối đến Gateway từ xa:
```bash
ssh -N -L 18789:127.0.0.1:18789 user@dia-chi-may-chu
```
Sau khi đường truyền được thiết lập, mọi lệnh `moltbot` trên máy laptop của bạn sẽ gửi đến máy chủ từ xa y như đang chạy tại máy đó.

## Cấu hình mặc định cho CLI
Bạn có thể lưu cấu hình để các lệnh `moltbot` luôn trỏ về máy chủ từ xa:
```json5
{
  "gateway": {
    "mode": "remote",
    "remote": {
      "url": "ws://127.0.0.1:18789",
      "token": "ma-token-cua-ban"
    }
  }
}
```

## Lưu ý về bảo mật
- **Luôn ưu tiên loopback**: Chỉ để Gateway lắng nghe ở địa chỉ `127.0.0.1` để tránh bị lộ ra internet công cộng.
- **Xác thực**: Luôn sử dụng Token hoặc mật khẩu khi bạn cho phép kết nối từ bên ngoài mạng nội bộ.

---
Tài liệu liên quan: [Tailscale](./tailscale.vi.md), [Bảo mật](./security/index.vi.md), [Nhiều Gateway](./multiple-gateways.vi.md).
