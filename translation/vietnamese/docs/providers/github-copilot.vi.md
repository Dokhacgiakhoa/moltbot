---
summary: "Đăng nhập và sử dụng GitHub Copilot cho mô hình AI trong Moltbot"
read_when:
  - Bạn muốn dùng GitHub Copilot làm bộ não cho bot của mình thông qua tài khoản cá nhân
---
# GitHub Copilot

GitHub Copilot không chỉ là một trợ lý lập trình trong VS Code, mà Moltbot còn có thể sử dụng các mô hình của nó (như GPT-4o) để làm bộ não cho Agent của bạn.

## Hai cách sử dụng Copilot trong Moltbot

### 1) Sử dụng trực tiếp (`github-copilot`) - Khuyên dùng
Đây là cách đơn giản nhất. Bạn sử dụng quy trình đăng nhập thiết bị (device-login) để cấp quyền cho Moltbot kết nối với GitHub. Bạn không cần phải mở VS Code để bot hoạt động.

### 2) Qua Plugin Copilot Proxy (`copilot-proxy`)
Sử dụng nếu bạn đang dùng tiện ích mở rộng Copilot Proxy trong VS Code như một cầu nối tại chỗ. Cách này yêu cầu bạn luôn phải mở VS Code.

## Thiết lập qua CLI (Dành cho cách thức trực tiếp)
Để bắt đầu, hãy chạy lệnh sau trong terminal của bạn:
```bash
moltbot models auth login-github-copilot
```
Hệ thống sẽ cung cấp một địa chỉ URL và một mã số. Bạn hãy truy cập URL đó, nhập mã số để xác nhận cấp quyền cho Moltbot.

## Chọn mô hình mặc định
Sau khi đăng nhập thành công, bạn có thể thiết lập mô hình muốn dùng (ví dụ: GPT-4o):
```bash
moltbot models set github-copilot/gpt-4o
```

## Các lưu ý quan trọng
- Bạn cần có gói đăng ký GitHub Copilot (cá nhân hoặc doanh nghiệp) đang hoạt động.
- Các mô hình khả dụng sẽ phụ thuộc vào gói đăng ký của bạn trên GitHub.
- Mã xác thực sẽ được lưu trữ an toàn trong hồ sơ của Moltbot để sử dụng cho các lần sau.

---
Tài liệu liên quan: [Xác thực OAuth](../../concepts/oauth.vi.md), [Lựa chọn mô hình](../../concepts/models.vi.md).
