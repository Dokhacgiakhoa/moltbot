---
summary: "Tài liệu tham khảo lệnh `moltbot plugins` (Liệt kê, Cài đặt, Bật/Tắt, Chẩn đoán)"
read_when:
  - Bạn muốn cài đặt hoặc quản lý các tiện ích mở rộng chạy trực tiếp trong Gateway
---

# `moltbot plugins`

Quản lý các tiện ích mở rộng (plugins) cho Gateway. Các plugin này được tải và chạy trực tiếp bên trong tiến trình của Gateway.

Tài liệu liên quan:
- Hệ thống Plugin: [Plugins](../../plugin.vi.md)
- Bảo mật hệ thống: [Bảo mật](../gateway/security/index.vi.md)

## Các lệnh chính

```bash
moltbot plugins list            # Xem danh sách plugins
moltbot plugins info <id>       # Xem chi tiết một plugin
moltbot plugins enable <id>     # Kích hoạt plugin
moltbot plugins disable <id>    # Tạm dừng plugin
moltbot plugins doctor         # Kiểm tra lý do plugin tải lỗi
moltbot plugins update --all    # Cập nhật tất cả các plugin
```

Các plugin đi kèm (bundled) thường mặc định ở trạng thái tắt. Bạn cần dùng lệnh `enable` để kích hoạt chúng khi cần thiết.

## Cài đặt Plugin mới

Bạn có thể cài đặt plugin từ một thư mục cục bộ, một file nén (.zip, .tgz) hoặc từ kho lưu trữ npm:

```bash
moltbot plugins install <đường-dẫn-hoặc-tên-package>
```

**Lưu ý về bảo mật**: Cài đặt một plugin tương đương với việc cho phép chạy mã nguồn lạ trên máy tính của bạn. Hãy chỉ cài đặt các plugin từ những nguồn mà bạn thực sự tin tưởng.

Hầu hết các thay đổi về plugin đều yêu cầu bạn khởi động lại Gateway để áp dụng.

---
Tài liệu liên quan: [Cấu hình Gateway](../gateway/configuration.vi.md).
