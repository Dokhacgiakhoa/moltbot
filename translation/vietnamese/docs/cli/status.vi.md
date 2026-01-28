---
summary: "Tài liệu tham khảo lệnh `moltbot status` (Chẩn đoán, thăm dò và kiểm tra dung lượng sử dụng)"
read_when:
  - Bạn muốn kiểm tra nhanh tình trạng các kênh và các phiên trò chuyện gần đây
---

# `moltbot status`

Lệnh chẩn đoán cho các kênh truyền thông và phiên làm việc (sessions).

## Ví dụ sử dụng

```bash
# Xem trạng thái cơ bản
moltbot status

# Xem báo cáo chẩn đoán đầy đủ (có thể dùng để gửi yêu cầu hỗ trợ)
moltbot status --all

# Thăm dò thực tế tình trạng kết nối của các kênh
moltbot status --deep

# Kiểm tra lưu lượng/hạn mức sử dụng của các nhà cung cấp AI
moltbot status --usage
```

## Các thành phần hiển thị:
- **Thăm dò sâu (`--deep`)**: Thực hiện kết nối thực tế tới WhatsApp, Telegram, Discord... để kiểm tra xem bot có thực sự đang trực tuyến không.
- **Dung lượng sử dụng**: Nếu bạn cung cấp mã API key, Moltbot sẽ hiển thị hạn mức còn lại từ các nhà cung cấp như Anthropic, OpenAI, Google Gemini...
- **Thông tin cập nhật**: Nếu có phiên bản mới, hệ thống sẽ hiển thị thông báo nhắc nhở bạn chạy lệnh `moltbot update`.

---
Tài liệu liên quan: [Khắc phục sự cố](../gateway/troubleshooting.vi.md), [Cập nhật hệ thống](../../install/updating.md).
