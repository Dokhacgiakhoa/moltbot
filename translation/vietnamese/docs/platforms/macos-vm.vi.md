---
summary: "Chạy Moltbot trong máy ảo macOS (cục bộ hoặc đám mây) khi bạn cần sự cô lập hoặc dùng iMessage"
read_when:
  - Bạn muốn tách biệt Moltbot khỏi môi trường làm việc chính trên máy Mac
  - Bạn muốn tích hợp iMessage (BlueBubbles) trong môi trường an toàn
  - Bạn muốn một môi trường macOS có thể sao lưu và khôi phục nhanh chóng
---

# Moltbot trên máy ảo macOS (Sandboxing)

## Lời khuyên lựa chọn (Dành cho hầu hết người dùng)

- **VPS Linux nhỏ**: Tiết kiệm chi phí nhất để chạy Gateway 24/7. Xem [Thuê máy chủ VPS](../../vps.vi.md).
- **Phần cứng riêng (Mac mini)**: Nếu bạn muốn toàn quyền kiểm soát và cần **IP dân cư** (Residential IP) để duyệt web tự động mà không bị chặn.
- **Máy ảo (VM)**: Chỉ dùng khi bạn cần tính năng chỉ có trên macOS (như iMessage) hoặc muốn cô lập hoàn toàn Bot khỏi dữ liệu cá nhân trên máy Mac chính.

## Các lựa chọn máy ảo macOS

### 1. Máy ảo cục bộ dùng Lume (Khuyên dùng cho chip Apple Silicon)
Bạn có thể chạy Moltbot trong một máy ảo macOS ngay trên máy chip M1/M2/M3 của mình bằng công cụ [Lume](https://cua.ai/docs/lume).
- **Ưu điểm**: Hoàn toàn miễn phí, cô lập tuyệt đối, hỗ trợ iMessage qua BlueBubbles.

### 2. Thuê máy Mac đám mây
Nếu bạn không có máy Mac hoặc muốn Bot luôn online, bạn có thể thuê từ các nhà cung cấp như **MacStadium**.

## Quy trình thiết lập nhanh bằng Lume

1. **Cài đặt Lume**:
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/trycua/cua/main/libs/lume/scripts/install.sh)"
   ```
2. **Tạo máy ảo**:
   ```bash
   lume create moltbot --os macos --ipsw latest
   ```
3. **Thiết lập macOS**: Hoàn tất các bước cài đặt macOS trong cửa sổ hiện lên, nhớ bật **Remote Login (SSH)** trong phần Sharing.
4. **Cài đặt Moltbot (bên trong máy ảo)**:
   ```bash
   ssh user@dia-chi-ip-may-ao
   npm install -g moltbot@latest
   moltbot onboard --install-daemon
   ```
5. **Chạy ngầm không cần màn hình**:
   ```bash
   lume stop moltbot
   lume run moltbot --no-display
   ```

## Tính năng iMessage (BlueBubbles)
Đây là lý do lớn nhất để chạy Moltbot trên macOS. Bằng cách cài đặt [BlueBubbles](https://bluebubbles.app) bên trong máy ảo, Agent của bạn sẽ có khả năng gửi và nhận tin nhắn iMessage y như một người dùng thật.

---
Tài liệu liên quan: [Cài đặt iMessage](../../channels/bluebubbles.vi.md), [Cài đặt Docker](../../install/docker.vi.md).
