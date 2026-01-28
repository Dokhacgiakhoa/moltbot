---
summary: "Danh sách kiểm tra phát hành Moltbot cho macOS (Cập nhật Sparkle, đóng gói, ký tên)"
read_when:
  - Bạn đang đóng gói một phiên bản Moltbot mới để phát hành cho người dùng Mac
---

# Phát hành Moltbot cho macOS (Sparkle)

Ứng dụng hiện hỗ trợ cơ chế tự động cập nhật qua Sparkle. Các bản phát hành chính thức phải được ký tên bằng **Developer ID**, đóng gói dạng ZIP/DMG và công bố thông qua tệp tin `appcast.xml`.

## Các bước chuẩn bị
1. **Chứng chỉ**: Phải có chứng chỉ `Developer ID Application` đã được cài đặt trên máy.
2. **Khóa Sparkle**: Phải có tệp khóa bí mật ed25519 (đường dẫn lưu trong biến môi trường `SPARKLE_PRIVATE_KEY_FILE`).
3. **Notarization**: Cấu hình tài khoản App Store Connect để Apple xác thực ứng dụng trước khi phát hành (giúp tránh cảnh báo phần mềm độc hại cho người dùng).

## Quy trình đóng gói
Chúng tôi sử dụng các kịch bản tự động để xây dựng phiên bản chính thức:

```bash
# Xây dựng và ký tên ứng dụng
BUNDLE_ID=bot.molt.mac \
APP_VERSION=2026.x.x \
BUILD_CONFIG=release \
scripts/package-mac-app.sh

# Tạo tệp tin cập nhật cho Sparkle
scripts/make_appcast.sh dist/Moltbot-2026.x.x.zip https://.../appcast.xml
```

## Lưu ý về phiên bản (APP_BUILD)
Giá trị `APP_BUILD` phải là một con số tăng dần (ví dụ dùng tổng số lần commit của Git). Sparkle dựa vào con số này để xác định xem người dùng có cần tải phiên bản mới hay không.

## Công bố
- Tải tệp tin ZIP và DMG lên mục **Releases** trên GitHub.
- Cập nhật tệp `appcast.xml` ở nhánh chính trên GitHub để ứng dụng của người dùng có thể nhận biết được bản cập nhật mới.

---
Tài liệu liên quan: [Thiết lập nhà phát triển](./dev-setup.vi.md), [Ứng dụng macOS](../macos.vi.md).
