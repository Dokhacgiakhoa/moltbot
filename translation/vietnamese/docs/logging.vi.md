---
summary: "Tổng quan về hệ thống nhật ký (logging): tệp nhật ký, đầu ra bảng điều khiển, theo dõi qua CLI và giao diện Control UI"
---

# Nhật ký hệ thống (Logging)

Moltbot ghi nhật ký tại hai nơi:

- **Tệp nhật ký** (File logs): Các dòng JSON được ghi bởi Gateway.
- **Đầu ra bảng điều khiển** (Console output): Hiển thị trong cửa sổ lệnh (terminal) và giao diện Control UI.

Trang này giải thích nơi lưu trữ nhật ký, cách đọc và cách cấu hình các cấp độ (level) cũng như định dạng của chúng.

## Nơi lưu trữ nhật ký

Mặc định, Gateway ghi tệp nhật ký luân phiên tại:

`/tmp/moltbot/moltbot-YYYY-MM-DD.log`

Bạn có thể thay đổi đường dẫn này trong tệp `~/.clawdbot/moltbot.json`:

```json
{
  "logging": {
    "file": "/path/to/moltbot.log"
  }
}
```

## Cách đọc nhật ký

### CLI: Theo dõi trực tiếp (Khuyên dùng)

Sử dụng lệnh sau để xem nhật ký theo thời gian thực:

```bash
moltbot logs --follow
```

Các chế độ đầu ra:
- `--json`: Xuất định dạng JSON (mỗi sự kiện là một dòng).
- `--plain`: Buộc xuất văn bản thuần (không màu sắc).
- `--no-color`: Tắt màu sắc ANSI.

Nếu Gateway không thể kết nối, hãy chạy lệnh:
`moltbot doctor`

### Giao diện Control UI (Web)

Trong giao diện Control UI, tab **Logs** sẽ hiển thị nội dung nhật ký tương tự. Xem [Giao diện Control UI](./web/control-ui.vi.md) để biết cách mở.

### Nhật ký theo kênh nhắn tin

Để lọc các hoạt động theo từng kênh (WhatsApp/Telegram/v.v.), sử dụng:

```bash
moltbot channels logs --channel whatsapp
```

## Cấu hình nhật ký

Toàn bộ cấu hình nhật ký nằm trong mục `logging` của tệp `moltbot.json`.

```json
{
  "logging": {
    "level": "info",
    "file": "/tmp/moltbot/moltbot-YYYY-MM-DD.log",
    "consoleLevel": "info",
    "consoleStyle": "pretty",
    "redactSensitive": "tools"
  }
}
```

### Các cấp độ nhật ký (Log levels)

- `logging.level`: Cấp độ ghi vào **tệp nhật ký**.
- `logging.consoleLevel`: Cấp độ hiển thị trên **bảng điều khiển**.

### Kiểu hiển thị trên bảng điều khiển

`logging.consoleStyle`:
- `pretty`: Thân thiện với con người, có màu sắc và mốc thời gian.
- `compact`: Đầu ra gọn gàng hơn (tốt cho các phiên làm việc dài).
- `json`: Định dạng JSON mỗi dòng.

### Làm sạch dữ liệu nhạy cảm (Redaction)

Moltbot có thể ẩn đi các thông tin nhạy cảm (như API key) trước khi in ra bảng điều khiển:
- `logging.redactSensitive`: Mặc định là `tools`.

## Chẩn đoán & OpenTelemetry

Hệ thống chẩn đoán (Diagnostics) là các sự kiện có cấu trúc dùng cho việc theo dõi hiệu năng và luồng tin nhắn.

### OpenTelemetry (OTel)
Moltbot hỗ trợ xuất dữ liệu chẩn đoán qua giao thức OTLP/HTTP để tích hợp với các hệ thống giám sát như Grafana, Honeycomb, v.v.

Các tín hiệu được xuất ra bao gồm:
- **Metrics**: Bộ đếm việc sử dụng Token, chi phí, luồng tin nhắn.
- **Traces**: Dấu vết sử dụng mô hình AI và quá trình xử lý tin nhắn.
- **Logs**: Xuất nhật ký hệ thống qua OTLP.

### Kích hoạt Nhật ký chẩn đoán chuyên sâu (Targeted logs)

Bạn có thể sử dụng các "cờ" (flags) để bật nhật ký debug cho từng phần cụ thể mà không cần tăng cấp độ nhật ký toàn hệ thống:

```json
{
  "diagnostics": {
    "flags": ["telegram.http"]
  }
}
```

---
Tài liệu liên quan: [Xử lý sự cố](./help/troubleshooting.vi.md), [Cấu hình Gateway](./gateway/configuration.vi.md).
