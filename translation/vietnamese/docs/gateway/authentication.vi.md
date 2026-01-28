---
summary: "Xác thực mô hình: OAuth, Khóa API và setup-token"
read_when:
  - Bạn muốn chẩn đoán lỗi đăng nhập hoặc hết hạn token của mô hình AI
---

# Xác thực (Authentication)

Moltbot hỗ trợ cả OAuth và Khóa API cho các nhà cung cấp mô hình. Đối với các tài khoản Anthropic, bạn nên sử dụng **Khóa API (API Key)**. Đối với quyền truy cập đăng ký Claude Pro/Max, hãy sử dụng token dài hạn được tạo bởi lệnh `claude setup-token`.

## Thiết lập Anthropic khuyên dùng (Khóa API)

Nếu bạn sử dụng Anthropic trực tiếp, hãy dùng Khóa API:

1) Tạo Khóa API trong Bảng điều khiển Anthropic (Anthropic Console).
2) Đưa khóa này lên máy chủ chạy Gateway.

```bash
export ANTHROPIC_API_KEY="..."
moltbot models status
```

3) Nếu Gateway chạy dưới dạng dịch vụ hệ thống (systemd/launchd), hãy đưa khóa vào tệp `~/.clawdbot/.env` để dịch vụ có thể đọc được:

```bash
echo "ANTHROPIC_API_KEY=..." >> ~/.clawdbot/.env
```

Sau đó khởi động lại tiến trình Gateway và kiểm tra lại bằng lệnh `moltbot doctor`.

## Anthropic: setup-token (Xác thực đăng ký)

Nếu bạn đang sử dụng gói đăng ký Claude Pro, hãy chạy lệnh sau trên máy chủ chạy Gateway:

```bash
claude setup-token
```

Sau đó dán mã thu được vào Moltbot:

```bash
moltbot models auth setup-token --provider anthropic
```

## Kiểm tra trạng thái xác thực

Sử dụng các lệnh sau để đảm bảo mọi thứ đã sẵn sàng:
- `moltbot models status`: Xem chi tiết các hồ sơ tài khoản và thời gian hết hạn.
- `moltbot doctor`: Kiểm tra tổng thể sức khỏe hệ thống và kết nối.

## Điều khiển định danh sử dụng

### Cho từng phiên làm việc
Bạn có thể ghim một tài khoản cụ thể cho cuộc trò chuyện hiện tại bằng lệnh:
`/model <tên-mô-hình>@<ID-hồ-sơ>` (ví dụ: `Opus@anthropic:work`).

### Cho từng Agent
Bạn có thể ép buộc thứ tự sử dụng tài khoản cho một Agent bằng lệnh:
```bash
moltbot models auth order set --provider anthropic anthropic:default
```

---
Tài liệu liên quan: [Khái niệm OAuth](../concepts/oauth.vi.md), [Dự phòng lỗi mô hình](../concepts/model-failover.vi.md).
