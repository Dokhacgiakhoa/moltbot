---
summary: "Giao diện theo dõi mức độ sử dụng và các yêu cầu về thông tin xác thực"
read_when:
  - Bạn đang thiết lập các giao diện hiển thị hạn mức/sử dụng của nhà cung cấp
---
# Theo dõi mức độ sử dụng (Usage tracking)

Moltbot có khả năng truy xuất trực tiếp thông tin về mức độ sử dụng và hạn mức (quota) từ các nhà cung cấp mô hình AI.

## Các vị trí hiển thị thông tin
- **Lệnh `/status` trong chat**: Hiển thị thẻ trạng thái với số lượng token của phiên hiện tại và chi phí ước tính (nếu dùng API key).
- **Lệnh `/usage tokens|full`**: Hiển thị thông tin sử dụng ở chân trang (footer) cho mỗi phản hồi của bot.
- **CLI**: Lệnh `moltbot status --usage` in ra báo cáo chi tiết cho từng nhà cung cấp.
- **Thanh menu macOS**: Mục "Usage" dưới phần Ngữ cảnh (nếu có hỗ trợ).

## Các nhà cung cấp được hỗ trợ
Thông tin sử dụng được truy xuất qua các hồ sơ xác thực (OAuth) hoặc API key cho:
- **Anthropic (Claude)**, **OpenAI (ChatGPT)**, **Google Gemini**, **GitHub Copilot**, **Antigravity**.
- **MiniMax**: Sử dụng API key, hỗ trợ hiển thị cửa sổ sử dụng của gói lập trình 5 giờ.
- **z.ai**: Sử dụng API key qua biến môi trường hoặc cấu hình.

Thông tin sử dụng sẽ được ẩn đi nếu Moltbot không tìm thấy thông tin xác thực tương ứng hoặc nhà cung cấp không hỗ trợ truy xuất qua API.

---
Tài liệu liên quan: [Cấu hình Gateway](../gateway/configuration.vi.md), [Cấu hình OAuth](./oauth.vi.md).
