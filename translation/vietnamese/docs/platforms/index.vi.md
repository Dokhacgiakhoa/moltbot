---
summary: "Tổng quan về hỗ trợ nền tảng (Gateway + ứng dụng đi kèm)"
read_when:
  - Bạn đang tìm hiểu về hệ điều hành hỗ trợ hoặc đường dẫn cài đặt
  - Bạn đang quyết định xem nên chạy Gateway ở đâu
---

# Nền tảng hỗ trợ (Platforms)

Mã nguồn cốt lõi của Moltbot được viết bằng TypeScript. **Node.js là môi trường chạy được khuyên dùng**.
Bun hiện không được khuyến khích dùng cho Gateway vì còn gặp lỗi với WhatsApp/Telegram.

Hiện đã có các ứng dụng đi kèm (companion apps) cho macOS (ứng dụng trên thanh menu) và các nút mạng di động (iOS/Android). Các ứng dụng cho Windows và Linux đang được lên kế hoạch phát triển, tuy nhiên bạn vẫn có thể chạy Gateway đầy đủ tính năng trên các nền tảng này ngay hôm nay.
Đối với Windows, ứng dụng bản địa (native app) cũng đang được phát triển; hiện tại chúng tôi khuyên dùng Gateway thông qua WSL2.

## Lựa chọn hệ điều hành của bạn

- macOS: [Hướng dẫn cho macOS](./macos.vi.md)
- iOS: [Hướng dẫn cho iOS](./ios.vi.md)
- Android: [Hướng dẫn cho Android](./android.vi.md)
- Windows: [Hướng dẫn cho Windows](./windows.vi.md)
- Linux: [Hướng dẫn cho Linux](./linux.vi.md)

## Máy chủ ảo (VPS) & Lưu trữ (Hosting)

- Trung tâm VPS: [Thuê máy chủ VPS](../../vps.vi.md)
- Fly.io: [Hướng dẫn Fly.io](./fly.vi.md)
- Hetzner (Docker): [Hướng dẫn Hetzner](./hetzner.vi.md)
- GCP (Compute Engine): [Hướng dẫn GCP](./gcp.vi.md)
- exe.dev (VM + HTTPS proxy): [Hướng dẫn exe.dev](./exe-dev.vi.md)

## Các liên kết phổ biến

- Bắt đầu nhanh: [Hướng dẫn cài đặt](../../start/getting-started.vi.md)
- Vận hành Gateway: [Gateway](../../gateway/index.vi.md)
- Cấu hình Gateway: [Cấu hình](../../gateway/configuration.vi.md)
- Trạng thái dịch vụ: `moltbot gateway status`

## Cài đặt dịch vụ Gateway (CLI)

Bạn có thể sử dụng một trong các cách sau (tất cả đều được hỗ trợ):

- Trình hướng dẫn (khuyên dùng): `moltbot onboard --install-daemon`
- Trực tiếp: `moltbot gateway install`
- Trình cấu hình: `moltbot configure` → chọn **Gateway service**
- Sửa lỗi/Di chuyển: `moltbot doctor` (sẽ đề xuất cài đặt hoặc sửa lỗi dịch vụ)

Tên dịch vụ phụ thuộc vào hệ điều hành:
- macOS: LaunchAgent (`bot.molt.gateway`)
- Linux/WSL2: systemd user service (`moltbot-gateway.service`)

---
Tài liệu liên quan: [Cài đặt](../../install/index.vi.md), [Xử lý sự cố](../../gateway/troubleshooting.vi.md).
