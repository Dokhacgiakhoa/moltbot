---
summary: "Trung tâm mạng: Các bề mặt của gateway, ghép nối, khám phá và bảo mật"
---
# Trung tâm Mạng hệ thống (Network hub)

Trang này liên kết các tài liệu cốt lõi về cách Moltbot kết nối, ghép nối (pairing) và bảo mật các thiết bị thông qua localhost, mạng nội bộ (LAN) và mạng Tailscale.

## Mô hình cốt lõi

- [Kiến trúc Gateway](../../concepts/architecture.vi.md)
- [Giao thức Gateway](../../gateway/protocol.vi.md)
- [Hướng dẫn vận hành Gateway](../../gateway/index.vi.md)
- [Bề mặt giao diện Web & Chế độ liên kết](../../web/index.vi.md)

## Ghép nối & Định danh (Pairing & Identity)

- [Tổng quan về Ghép nối (DM + Nút mạng)](../../start/pairing.vi.md)
- [Ghép nối nút mạng thuộc quyền Gateway](../../gateway/pairing.vi.md)
- [CLI cho thiết bị (Ghép nối & đổi mã token)](../../cli/devices.vi.md)

**Tin cậy nội bộ:**
- Các kết nối nội bộ (vòng lặp hoặc địa chỉ Tailscale của chính máy chủ Gateway) có thể được tự động phê duyệt để mang lại trải nghiệm mượt mà.
- Các thiết bị khác từ Tailscale/LAN vẫn yêu cầu phê duyệt ghép nối rõ ràng.

## Khám phá & Truyền tải (Discovery & Transports)

- [Khám phá & Truyền tải](../../gateway/discovery.vi.md)
- [Bonjour / mDNS](../../gateway/bonjour.vi.md)
- [Truy cập từ xa (SSH)](../../gateway/remote.vi.md)
- [Tailscale](../../gateway/tailscale.vi.md)

## Nút mạng & Truyền tải (Nodes & Transports)

- [Tổng quan về Nút mạng](../../nodes/index.vi.md)
- [Giao thức Bridge (Dành cho các nút mạng cũ)](../../gateway/bridge-protocol.vi.md)
- [Hướng dẫn cho iOS](../../platforms/ios.vi.md)
- [Hướng dẫn cho Android](../../platforms/android.vi.md)

## Bảo mật

- [Tổng quan về Bảo mật](../../gateway/security.vi.md)
- [Tham chiếu Cấu hình Gateway](../../gateway/configuration.vi.md)
- [Xử lý sự cố](../../help/troubleshooting.vi.md)
- [Sửa chữa lỗi (Doctor)](../../gateway/doctor.vi.md)
