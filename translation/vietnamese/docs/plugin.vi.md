---
summary: "Plugin và tiện ích mở rộng của Moltbot: Cách khám phá, cấu hình và đảm bảo an toàn"
---

# Plugin (Tiện ích mở rộng)

## Bắt đầu nhanh (Plugin là gì?)

Plugin là các **mô-đun mã nguồn nhỏ** giúp mở rộng tính năng cho Moltbot (bổ sung lệnh, công cụ và các hàm Gateway RPC). Bạn sẽ cần dùng đến plugin khi muốn có một tính năng mà Moltbot chưa có sẵn hoặc muốn tách biệt các tính năng tùy chọn ra khỏi bản cài đặt chính.

Các bước nhanh:
1. Xem danh sách plugin hiện có: `moltbot plugins list`
2. Cài đặt plugin chính thức (ví dụ: Voice Call):
   `moltbot plugins install @moltbot/voice-call`
3. Khởi động lại Gateway, sau đó cấu hình chúng trong mục `plugins.entries.<id>.config` của tệp cài đặt.

## Các plugin chính thức hiện có

- **Microsoft Teams**: Dưới dạng plugin độc lập `@moltbot/msteams`.
- **Memory (Hệ thống/LanceDB)**: Plugin quản lý bộ nhớ dài hạn (mặc định đã được bật).
- **Voice Call**: Thực hiện cuộc gọi thoại qua Twilio.
- **Zalo Personal**: Kết nối với tài khoản Zalo cá nhân.
- **Matrix / Nostr / Zalo**: Các kênh nhắn tin mở rộng.

## Khả năng của Plugin

Plugin có thể đăng ký:
- Các phương thức điều khiển Gateway (Gateway RPC).
- Các công cụ cho Agent (Agent tools).
- Các lệnh dòng lệnh (CLI).
- Các dịch vụ chạy ngầm.
- **Kỹ năng (Skills)**: Thêm các kỹ năng mới vào mã nguồn.
- **Lệnh tự động trả lời**: Thực thi ngay lập tức mà không cần gọi đến mô hình AI (như lệnh kiểm tra trạng thái).

## Cách Moltbot tìm kiếm Plugin

Hệ thống sẽ quét theo thứ tự ưu tiên:
1. Đường dẫn tùy chỉnh trong cấu hình (`plugins.load.paths`).
2. Tiện ích của không gian làm việc (`<workspace>/.clawdbot/extensions/`).
3. Tiện ích toàn cục (`~/.clawdbot/extensions/`).
4. Tiện ích đi kèm (bundled) trong bộ cài Moltbot.

Mỗi plugin bắt buộc phải có tệp `moltbot.plugin.json` ở thư mục gốc để mô tả thông tin và sơ đồ cấu hình (schema).

## Khe cắm Plugin (Plugin Slots)

Một số danh mục plugin mang tính **độc quyền** (chỉ một cái được hoạt động tại một thời điểm). Ví dụ, bạn dùng `plugins.slots.memory` để chọn xem plugin bộ nhớ nào sẽ được kích hoạt (mặc định là `memory-core`).

## Các lệnh điều khiển qua CLI

- `moltbot plugins list`: Liệt kê plugin.
- `moltbot plugins install <đường dẫn/tên>`: Cài đặt plugin mới (từ thư mục, tệp zip hoặc npm).
- `moltbot plugins enable/disable <id>`: Bật hoặc tắt plugin.
- `moltbot plugins update`: Cập nhật các plugin đã cài qua npm.

## Lưu ý về an toàn

Plugin chạy ngay trong tiến trình của Gateway. Bạn nên:
- Chỉ cài đặt các plugin từ nguồn tin cậy.
- Sử dụng danh sách cho phép (`plugins.allow`) để kiểm soát các plugin được phép chạy.
- Luôn khởi động lại Gateway sau khi cài đặt hoặc thay đổi cấu hình plugin.

---
Tài liệu liên quan: [Kỹ năng](../tools/skills.vi.md), [Cấu hình Gateway](../gateway/configuration.vi.md), [Xác thực mô hình](../concepts/oauth.vi.md).
