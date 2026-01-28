---
summary: "Bảng vẽ (Canvas) do Agent điều khiển, được nhúng qua WKWebView trên macOS"
read_when:
  - Bạn đang phát triển tính năng Bảng vẽ trên macOS
  - Bạn muốn hiểu cách AI tương tác với không gian hiển thị hình ảnh
---

# Bảng vẽ Canvas (Ứng dụng macOS)

Ứng dụng macOS tích hợp một **bảng vẽ Canvas** do Agent điều khiển bằng công nghệ `WKWebView`. Đây là một không gian làm việc trực quan nhẹ nhàng để hiển thị HTML/CSS/JS và các giao diện tương tác nhỏ.

## Vị trí lưu trữ dữ liệu
Dữ liệu của Canvas được lưu trong thư mục Application Support:
- `~/Library/Application Support/Moltbot/canvas/<phiên>/...`

Ứng dụng sử dụng một giao thức URL riêng để truy cập các tệp này:
- `moltbot-canvas://<phiên>/<đường-dẫn>`

## Hành vi của bảng vẽ
- Là một cửa sổ không viền, có thể thay đổi kích thước và được đính gần thanh menu hoặc con trỏ chuột.
- Tự động ghi nhớ vị trí và kích thước cho từng phiên làm việc.
- Tự động tải lại nội dung khi các tệp tin dưới máy thay đổi.

Bạn có thể bật/tắt tính năng này trong phần **Settings → Allow Canvas**.

## Cách Agent tương tác với Canvas
Agent có thể điều khiển Canvas thông qua kết nối WebSocket của Gateway để:
- Hiện hoặc ẩn bảng vẽ.
- Điều hướng tới một đường dẫn hoặc trang web.
- Chạy mã JavaScript trực tiếp trên trang.
- Chụp ảnh màn hình nội dung trên bảng vẽ.

**Ví dụ lệnh CLI:**
```bash
moltbot nodes canvas present --node <id>        # Hiện bảng vẽ
moltbot nodes canvas navigate --node <id> --url "/" # Về trang mặc định
```

## Bảo mật
- Canvas ngăn chặn việc truy cập vào các thư mục hệ thống khác (directory traversal); các tệp phải nằm trong thư mục gốc của phiên làm việc.
- Các trang web bên ngoài (`http/https`) chỉ được phép truy cập khi được lệnh điều hướng rõ ràng từ Agent.

---
Tài liệu liên quan: [Ứng dụng macOS](../macos.vi.md), [Giao diện A2UI](../../nodes/a2ui.vi.md).
