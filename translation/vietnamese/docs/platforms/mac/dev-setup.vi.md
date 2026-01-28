---
summary: "Hướng dẫn thiết lập dành cho nhà phát triển ứng dụng Moltbot trên macOS"
read_when:
  - Bạn đang chuẩn bị môi trường lập trình để đóng góp mã nguồn cho ứng dụng Mac
---

# Thiết lập môi trường phát triển trên macOS

Hướng dẫn này bao gồm các bước cần thiết để xây dựng và chạy ứng dụng Moltbot trên macOS từ mã nguồn.

## Yêu cầu chuẩn bị
Trước khi bắt đầu, hãy đảm bảo bạn đã cài đặt:
1. **Xcode 16.2+**: Bắt buộc để lập trình Swift.
2. **Node.js 22+ & pnpm**: Dùng cho Gateway, CLI và các kịch bản đóng gói.

## 1. Cài đặt phụ thuộc
Chạy lệnh sau tại thư mục gốc của dự án:
```bash
pnpm install
```

## 2. Xây dựng và Đóng gói ứng dụng
Để biên dịch ứng dụng macOS và đóng gói vào thư mục `dist/Moltbot.app`, hãy chạy:
```bash
./scripts/package-mac-app.sh
```
Nếu bạn không có chứng chỉ Apple Developer ID, kịch bản sẽ tự động sử dụng **chữ ký ad-hoc** (`-`).

## 3. Cài đặt CLI
Ứng dụng macOS cần có CLI `moltbot` được cài đặt toàn cục để quản lý các tác vụ ngầm.
- Mở ứng dụng Moltbot.
- Vào tab **General** trong phần cài đặt.
- Nhấn **"Install CLI"**.

## Xử lý sự cố
- **Lỗi biên dịch**: Hãy kiểm tra phiên bản Xcode và Swift của bạn bằng lệnh `xcodebuild -version`.
- **Ứng dụng bị sập khi cấp quyền**: Nếu ứng dụng văng khi bạn nhấn cho phép dùng Micro hoặc Nhận dạng giọng nói, hãy thử đặt lại quyền hạn TCC bằng lệnh: `tccutil reset All bot.molt.mac.debug`.
- **Gateway bị treo ở trạng thái "Starting..."**: Có thể một tiến trình cũ đang chiếm giữ cổng. Hãy kiểm tra bằng lệnh `lsof -nP -iTCP:18789 -sTCP:LISTEN`.

---
Tài liệu liên quan: [Đánh giá sức khỏe](./health.vi.md), [Cấu hình hệ thống](../../gateway/configuration.vi.md).
