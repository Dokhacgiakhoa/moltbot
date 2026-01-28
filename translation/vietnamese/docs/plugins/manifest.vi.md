---
summary: "Tệp mô tả Plugin (manifest) và các yêu cầu về JSON schema (xác thực cấu hình nghiêm ngặt)"
read_when:
  - Bạn đang xây dựng một plugin mới cho Moltbot
---

# Tệp mô tả Plugin (moltbot.plugin.json)

Mọi plugin **bắt buộc** phải có một tệp `moltbot.plugin.json` nằm tại thư mục gốc của plugin đó. Moltbot sử dụng tệp này để xác thực các cài đặt cấu hình của plugin **mà không cần chạy mã nguồn của plugin**. Nếu tệp này bị thiếu hoặc không hợp lệ, plugin sẽ bị báo lỗi và không thể hoạt động.

## Các trường thông tin bắt buộc

```json
{
  "id": "voice-call",
  "configSchema": {
    "type": "object",
    "additionalProperties": false,
    "properties": {}
  }
}
```

- **id**: Định danh duy nhất của plugin.
- **configSchema**: Cấu trúc JSON Schema dùng để kiểm tra các cài đặt của plugin.

## Các trường thông tin tùy chọn
- **kind**: Loại plugin (ví dụ: "memory").
- **channels**: Danh sách các kênh nhắn tin mà plugin này cung cấp (ví dụ: ["matrix"]).
- **name**: Tên hiển thị của plugin.
- **description**: Mô tả ngắn gọn về tính năng của plugin.
- **version**: Phiên bản của plugin.

## Các lưu ý quan trọng
- Ngay cả khi plugin của bạn không yêu cầu cài đặt gì, bạn vẫn phải cung cấp một `configSchema` trống.
- Bảng điều khiển (Control UI) sẽ dựa vào tệp này để hiển thị các ô nhập liệu cấu hình cho người dùng một cách chính xác.

---
Tài liệu liên quan: [Cấu hình Gateway](../../gateway/configuration.vi.md), [Hệ thống Plugin](./index.vi.md).
