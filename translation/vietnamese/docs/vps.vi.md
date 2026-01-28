---
summary: "Trung tâm lưu trữ VPS cho Moltbot (Oracle/Fly/Hetzner/GCP/v.v.)"
---

# Lưu trữ VPS (VPS hosting)

Trang này cung cấp các hướng dẫn về cách triển khai Moltbot trên các nhà cung cấp VPS/Cloud phổ biến.

## Lựa chọn nhà cung cấp

- **Railway** (Cài đặt một chạm): [Hướng dẫn Railway](./railway.vi.mdx).
- **Northflank** (Cài đặt một chạm): [Hướng dẫn Northflank](./northflank.vi.mdx).
- **Oracle Cloud (Miễn phí trọn đời)**: [Hướng dẫn Oracle](../platforms/oracle.vi.md) — Miễn phí $0/tháng (ARM).
- **Fly.io**: [Hướng dẫn Fly.io](../platforms/fly.vi.md).
- **Hetzner (Docker)**: [Hướng dẫn Hetzner](../platforms/hetzner.vi.md).
- **GCP (Compute Engine)**: [Hướng dẫn GCP](../platforms/gcp.vi.md).
- **AWS (EC2/Lightsail)**: Hoạt động rất tốt, phù hợp cho người dùng muốn tùy chỉnh sâu.

## Cơ chế hoạt động của Cloud

- **Gateway chạy trên VPS** và lưu giữ toàn bộ dữ liệu trạng thái cũng như không gian làm việc.
- Bạn kết nối từ máy tính/điện thoại cá nhân qua **Giao diện điều khiển (Control UI)**, **Tailscale** hoặc **SSH**.
- Hãy luôn **sao lưu** thư mục trạng thái và không gian làm việc trên VPS.
- **Bảo mật**: Khuyên dùng SSH tunnel hoặc Tailscale để truy cập Gateway. Nếu bạn mở cổng công khai, bắt buộc phải đặt `gateway.auth.token` hoặc mật khẩu.

## Kết nối Nút mạng (Nodes) với VPS

Bạn có thể treo Gateway trên Cloud 24/7 và ghép nối với các **nút mạng** trên thiết bị cá nhân (Mac/iOS/Android). Các nút mạng này cung cấp khả năng điều khiển màn hình/camera/vẽ hình cục bộ trong khi Gateway vẫn nằm trên đám mây.

---
Tài liệu liên quan: [Các nền tảng](../platforms/index.vi.md), [Truy cập từ xa](../gateway/remote.vi.md), [Nút mạng](../nodes/index.vi.md).
