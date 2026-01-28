---
summary: "Hướng dẫn cài đặt Moltbot trên Oracle Cloud (Gói Always Free ARM cực mạnh)"
read_when:
  - Bạn muốn sở hữu một VPS cấu hình cao (24GB RAM) hoàn toàn miễn phí
  - Bạn có tài khoản Oracle Cloud và muốn tận dụng chip ARM Ampere
---

# Moltbot trên Oracle Cloud (OCI)

Oracle Cloud cung cấp gói **Always Free** cực kỳ hào phóng với chip ARM (lên tới 4 CPU và 24GB RAM), rất phù hợp để chạy Moltbot Gateway 24/7 mà không tốn một xu nào.

## Các bước thiết lập

1. **Tạo máy ảo (Instance)**:
   - Hệ điều hành: Ubuntu 24.04 (aarch64).
   - Loại máy: `VM.Standard.A1.Flex`.
   - Cấu hình: Nên chọn ít nhất 2 CPU và 12GB RAM (vẫn nằm trong mức miễn phí).
2. **Cài đặt Tailscale**: Đây là cách an toàn nhất để kết nối tới máy chủ Oracle mà không cần mở cổng tường lửa công khai.
3. **Cài đặt Moltbot**:
   ```bash
   curl -fsSL https://molt.bot/install.sh | bash
   ```
4. **Bảo mật**: Khóa toàn bộ cổng trên bảng điều khiển Oracle (VCN Security), chỉ để lại cổng UDP cho Tailscale.

## Tại sao nên dùng phương án này?
- **Siêu mạnh**: 24GB RAM là mức cấu hình mà các bên khác sẽ thu phí ít nhất $40-$80 mỗi tháng.
- **Bảo mật**: Kết hợp với Tailscale, máy chủ của bạn sẽ hoàn toàn ẩn mình trước các chương trình quét cổng trên internet.

## Lưu ý về chip ARM
Vì đây là kiến trúc ARM, một số công cụ (binaries) cũ có thể không chạy được. Tuy nhiên, hầu hết các gói mã nguồn của Moltbot (Node.js) đều hoạt động hoàn hảo.

---
Tài liệu liên quan: [Tích hợp Tailscale](../../gateway/tailscale.vi.md), [Thuê máy chủ VPS](../../vps.vi.md).
