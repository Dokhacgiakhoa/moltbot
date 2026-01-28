---
summary: "Giao diện công cụ của Agent cho Moltbot (trình duyệt, canvas, nodes, tin nhắn, cron)"
read_when:
  - Thêm hoặc sửa đổi các công cụ của agent
---
# Công cụ (Tools)

Moltbot cung cấp các **công cụ agent chuyên dụng** cho trình duyệt, canvas, các nút (nodes) và tác vụ định kỳ (cron). Các công cụ này thay thế cho mô hình "kỹ năng" cũ: chúng có kiểu dữ liệu chặt chẽ và agent có thể sử dụng chúng trực tiếp.

## Tắt/Bật công cụ

Bạn có thể cho phép hoặc chặn các công cụ trên toàn hệ thống thông qua `tools.allow` / `tools.deny` trong file `moltbot.json`.

```json5
{
  tools: { deny: ["browser"] } // Chặn công cụ trình duyệt
}
```

## Nhóm công cụ (Shorthands)

Bạn có thể dùng các tên nhóm để đại diện cho nhiều công cụ cùng lúc:
- `group:runtime`: `exec`, `bash`, `process` (Chạy lệnh hệ thống)
- `group:fs`: `read`, `write`, `edit`, `apply_patch` (Thao tác file)
- `group:sessions`: Quản lý các phiên chat và lịch sử.
- `group:memory`: Tìm kiếm và đọc bộ nhớ.
- `group:web`: Tìm kiếm và đọc nội dung web.
- `group:ui`: Trình duyệt và giao diện canvas.
- `group:messaging`: Gửi tin nhắn qua các kênh.

## Danh sách công cụ tiêu biểu

### `exec`
Chạy các lệnh shell trong không gian làm việc.
- Cho phép agent thực thi code, cài đặt thư viện hoặc kiểm tra hệ thống.
- Có thể chạy ngầm (background) cho các tác vụ tốn thời gian.

### `web_search` & `web_fetch`
- `web_search`: Tìm kiếm web bằng Brave Search API.
- `web_fetch`: Lấy nội dung trang web và chuyển thành Markdown/Văn bản.

### `browser`
Điều khiển một trình duyệt chuyên dụng để tự động hóa web.
- Có thể chụp ảnh màn hình, nhấp chuột, nhập liệu, và phân tích cấu trúc trang web.
- Hỗ trợ nhiều cấu hình (profiles) khác nhau.

### `message`
Gửi tin nhắn và thực hiện các hành động trên các kênh: Discord, Google Chat, Slack, Telegram, WhatsApp, Signal, iMessage...
- Hỗ trợ gửi văn bản, media, tạo bình chọn (polls), thả cảm xúc (reactions), v.v.

### `sessions_list` / `sessions_history` / `sessions_send`
Quản lý các phiên chat: liệt kê, xem lịch sử hoặc gửi tin nhắn sang một phiên chat khác (điều hướng tin nhắn giữa các agent).

## An toàn
- Hạn chế sử dụng `exec` trực tiếp; chỉ cấp quyền thực thi lệnh hệ thống cho các agent tin cậy.
- Sử dụng sandbox để cô lập agent khi cần chạy các công cụ rủi ro cao.

---
Tài liệu liên quan: [Kỹ năng](./skills.vi.md), [Sandboxing](../gateway/sandboxing.vi.md).
