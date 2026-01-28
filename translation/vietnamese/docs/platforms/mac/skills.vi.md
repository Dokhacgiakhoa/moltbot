---
summary: "Giao diện quản lý Kỹ năng (Skills) và trạng thái từ Gateway trên macOS"
read_when:
  - Bạn muốn cài đặt thêm các kỹ năng mới cho Bot thông qua ứng dụng Mac
---

# Kỹ năng (macOS)

Ứng dụng macOS hiển thị danh sách các kỹ năng của Moltbot thông qua kết nối với Gateway; nó không tự xử lý các kỹ năng này tại địa phương.

## Nguồn dữ liệu
- Mọi thông tin về kỹ năng, tính hợp lệ và các yêu cầu hệ thống còn thiếu đều được lấy từ lệnh `skills.status` của Gateway.
- Các yêu cầu này được định nghĩa trong mục `metadata.moltbot.requires` của từng tệp `SKILL.md`.

## Hành động cài đặt
- Khi bạn nhấn cài đặt một kỹ năng, ứng dụng sẽ gọi lệnh `skills.install` để Gateway thực hiện việc cài đặt trên máy chủ (có thể là dùng `brew`, `npm`, `go`, v.v.).
- Nếu có nhiều phương thức cài đặt, hệ thống sẽ ưu tiên các phương thức phổ biến (như `brew` trên Mac).

## Chế độ điều khiển từ xa
Lưu ý rằng ở chế độ **Remote mode**, việc cài đặt và cấu hình kỹ năng sẽ diễn ra trên máy chủ Gateway chứ không phải trên máy Mac bạn đang cầm.

---
Tài liệu liên quan: [Ứng dụng macOS](../macos.vi.md), [Cấu hình Gateway](../../gateway/configuration.vi.md).
