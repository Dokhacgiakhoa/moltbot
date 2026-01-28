---
summary: "Ứng dụng iOS (Nút mạng): Kết nối với Gateway, ghép nối, canvas và xử lý sự cố"
read_when:
  - Bạn đang ghép nối hoặc kết nối lại thiết bị iOS
  - Bạn đang chạy thử ứng dụng iOS từ mã nguồn
---

# Ứng dụng iOS (Nút mạng)

Trạng thái: Đang thử nghiệm nội bộ. Ứng dụng iOS hiện chưa được phát hành rộng rãi trên App Store.

## Tính năng chính
- Kết nối tới Gateway qua WebSocket (mạng LAN hoặc mạng ảo Tailscale).
- Cung cấp các khả năng cho nút mạng: Hiển thị Canvas, Chụp màn hình, Chụp ảnh camera, Định vị, Chế độ đàm thoại và Đánh thức bằng giọng nói.
- Nhận các lệnh điều khiển `node.invoke` từ Agent.

## Yêu cầu
- Đã chạy Gateway trên một thiết bị khác (macOS, Linux hoặc Windows qua WSL2).
- Đường truyền mạng:
  - Cùng mạng LAN (qua Bonjour).
  - Hoặc qua mạng Tailscale.
  - Hoặc nhập địa chỉ IP thủ công.

## Bắt đầu nhanh (Ghép nối + Kết nối)

1. **Khởi động Gateway** trên máy tính:
   ```bash
   moltbot gateway --port 18789
   ```

2. **Trên điện thoại iOS**, mở mục Settings và chọn máy chủ Gateway tìm thấy được (hoặc nhập thủ công).

3. **Phê duyệt ghép nối** trên máy tính:
   ```bash
   moltbot nodes pending
   moltbot nodes approve <requestId>
   ```

4. **Kiểm tra kết nối**:
   ```bash
   moltbot nodes status
   ```

## Các lỗi thường gặp
- `NODE_BACKGROUND_UNAVAILABLE`: Hãy mở ứng dụng iOS lên màn hình chính (các lệnh canvas/camera/màn hình yêu cầu ứng dụng phải đang hiển thị phía trước).
- `A2UI_HOST_NOT_CONFIGURED`: Gateway chưa được cấu hình máy chủ Canvas; hãy kiểm tra lại file `moltbot.json`.
- Yêu cầu ghép nối không xuất hiện: Hãy chạy lệnh `moltbot nodes pending` để kiểm tra và phê duyệt thủ công.

---
Tài liệu liên quan: [Ghép nối](../../gateway/pairing.vi.md), [Tìm kiếm thiết bị](../../gateway/discovery.vi.md).
