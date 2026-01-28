---
summary: "Phân tích cú pháp vị trí từ các kênh chat (Telegram + WhatsApp) và các trường bối cảnh (context fields)"
read_when:
  - Bạn muốn sử dụng tọa độ vị trí trong các câu lệnh của AI
---
# Phân tích vị trí từ kênh truyền thông

Moltbot chuẩn hóa các dữ liệu vị trí được chia sẻ từ các kênh chat thành:
1. **Dạng văn bản dễ đọc**: Được thêm trực tiếp vào nội dung tin nhắn gửi tới AI.
2. **Dạng dữ liệu cấu trúc**: Được điền vào các trường trong `context` để AI có thể sử dụng cho các công cụ (như bản đồ, dự báo thời tiết...).

## Các kênh hỗ trợ hiện tại
- **Telegram**: Ghim vị trí, địa điểm cụ thể và vị trí trực tiếp (live location).
- **WhatsApp**: Chia sẻ vị trí và vị trí trực tiếp.
- **Matrix**: Vị trí dựa trên cú pháp `geo_uri`.

## Định dạng hiển thị
Các vị trí sẽ được hiển thị cho AI dưới dạng các dòng mô tả thân thiện:
- **Vị trí ghim**: `📍 48.858844, 2.294351 ±12m`
- **Địa điểm có tên**: `📍 Tháp Eiffel — Paris (48.858844, 2.294351 ±12m)`
- **Vị trí trực tiếp**: `🛰 Vị trí trực tiếp: 48.858844, 2.294351 ±12m`

## Các trường dữ liệu trong Context (`ctx`)
Khi nhận được tin nhắn chứa vị trí, Moltbot sẽ tự động điền các thông tin sau vào biến bối cảnh:
- `LocationLat`: Vĩ độ.
- `LocationLon`: Kinh độ.
- `LocationAccuracy`: Độ chính xác (tính bằng mét).
- `LocationName`: Tên địa điểm (nếu có).
- `LocationAddress`: Địa chỉ cụ thể (nếu có).
- `LocationIsLive`: Có phải đang chia sẻ trực tiếp hay không.

Thông tin này cực kỳ hữu ích nếu bạn viết các kỹ năng (skills) yêu cầu biết vị trí của người dùng hiện tại để xử lý dữ liệu.

---
Tài liệu liên quan: [Cấu hình hệ thống](../gateway/configuration.vi.md).
