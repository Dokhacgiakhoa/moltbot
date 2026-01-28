---
summary: "Cài đặt Moltbot theo phương pháp khai báo với Nix"
read_when:
  - Bạn muốn cài đặt có khả năng tái lập và dễ dàng khôi phục (rollback)
  - Bạn đang sử dụng NixOS hoặc Home Manager
---

# Cài đặt qua Nix

Cách khuyên dùng để chạy Moltbot với Nix là thông qua **[nix-moltbot](https://github.com/moltbot/nix-moltbot)** — một module tích hợp sẵn cho Home Manager.

## Bắt đầu nhanh
Hãy gửi yêu cầu sau cho trợ lý AI của bạn (Claude, Cursor, v.v.):
```text
Tôi muốn thiết lập nix-moltbot trên máy Mac của mình.
Kho lưu trữ: github:moltbot/nix-moltbot

Những gì tôi cần bạn làm:
1. Kiểm tra xem Nix đã được cài đặt chưa (nếu chưa, hãy cài đặt Determinate Nix).
2. Tạo một flake cục bộ tại ~/code/moltbot-local.
3. Thiết lập các khóa bí mật (API key) vào thư mục ~/.secrets/.
4. Điền các thông tin vào mẫu và chạy 'home-manager switch'.
5. Xác thực xem dịch vụ đã chạy và Bot đã phản hồi chưa.
```

> **📦 Hướng dẫn đầy đủ: [github.com/moltbot/nix-moltbot](https://github.com/moltbot/nix-moltbot)**

## Những gì bạn sẽ nhận được
- **Đầy đủ công cụ**: Gateway, ứng dụng macOS và các công cụ hỗ trợ (Whisper, Spotify, Camera) đều được ghim phiên bản cố định.
- **Dịch vụ tự chạy**: Tự động khởi động lại sau khi máy mở.
- **Hoàn tác tức thì**: Có thể quay lại phiên bản trước đó chỉ với một lệnh `home-manager switch --rollback`.

## Chế độ Nix (Nix Mode)
Khi chạy trong môi trường Nix, Moltbot sẽ tự động chuyển sang "Chế độ Nix". Ở chế độ này, các tính năng tự động cập nhật hoặc tự sửa lỗi mã nguồn sẽ bị tắt để đảm bảo tính nhất quán của hệ thống Nix.

Bạn có thể nhận biết Bot đang ở chế độ này thông qua dòng chữ "Nix mode" hiển thị trên giao diện người dùng.

---
Tài liệu liên quan: [Cài đặt Docker](./docker.vi.md), [Trình hướng dẫn thiết lập](../start/wizard.vi.md).
