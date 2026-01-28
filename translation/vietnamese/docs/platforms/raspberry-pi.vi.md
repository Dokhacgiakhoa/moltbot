---
summary: "Cài đặt Moltbot trên Raspberry Pi (Giải pháp tự lưu trữ tiết kiệm nhất)"
read_when:
  - Bạn muốn biến Raspberry Pi thành một trợ lý AI cá nhân luôn online tại nhà
  - Bạn muốn tiết kiệm chi phí thuê máy chủ hàng tháng
---

# Moltbot trên Raspberry Pi

Chạy Moltbot trên Raspberry Pi là cách tuyệt vời để có một trợ lý AI luôn sẵn sàng tại nhà với chi phí vận hành cực thấp (chỉ tốn tiền điện).

## Tóm tắt phần cứng

| Model | RAM | Đánh giá | Ghi chú |
|----------|-----|--------|-------|
| **Pi 5** | 4GB/8GB | ✅ Tốt nhất | Nhanh, khuyên dùng |
| **Pi 4** | 4GB | ✅ Ổn | Phù hợp cho hầu hết người dùng |
| **Pi 4** | 1GB/2GB | ⚠️ Tạm được | Cần thêm SWAP để tránh treo máy |

**Yêu cầu tối thiểu**: Hệ điều hành 64-bit là bắt buộc để chạy Node.js ổn định.

## Các bước thực hiện

1. **Cài đặt hệ điều hành**: Dùng **Raspberry Pi OS Lite (64-bit)** để tiết kiệm tài nguyên.
2. **Thiết lập bộ nhớ ảo (SWAP)**: Đây là bước **quan trọng nhất** trên Pi để tránh sập nguồn khi Bot xử lý nhiều dữ liệu. Hãy tạo ít nhất 2GB SWAP.
3. **Cài đặt Moltbot**:
   ```bash
   curl -fsSL https://molt.bot/install.sh | bash
   moltbot onboard --install-daemon
   ```
4. **Kết nối từ xa**: Sử dụng **Tailscale** để bạn có thể nhắn tin cho Bot ngay cả khi không ở nhà mà không cần mở cổng modem (Port forwarding).

## Lưu ý đặc biệt cho chip ARM
Hầu hết các tính năng của Moltbot đều hoạt động tốt trên kiến trúc ARM64 của Pi. Tuy nhiên, nếu bạn cài đặt thêm các công cụ bên ngoài (như FFmpeg hoặc Chromium), hãy luôn chọn phiên bản dành cho ARM64.

---
Tài liệu liên quan: [Hướng dẫn Linux](./linux.vi.md), [Tích hợp Tailscale](../../gateway/tailscale.vi.md).
