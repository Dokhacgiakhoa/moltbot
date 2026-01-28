---
summary: "Hooks: Tự động hóa dựa trên sự kiện cho các lệnh và vòng đời của Agent"
---
# Hooks (Móc nối sự kiện)

Hooks cung cấp một hệ thống tự động hóa dựa trên sự kiện để thực hiện các hành động mỗi khi có lệnh hoặc sự kiện từ Agent. Các Hook được tự động khám phá từ các thư mục và có thể được quản lý qua các lệnh CLI, tương tự như cách hoạt động của Kỹ năng (Skills).

## Định hướng

Hooks là những đoạn mã nhỏ chạy khi có điều gì đó xảy ra. Có hai loại chính:

- **Hooks** (Trang này): Chạy bên trong Gateway khi các sự kiện của Agent được kích hoạt, như `/new`, `/reset`, `/stop`, hoặc các sự kiện vòng đời hệ thống.
- **Webhooks**: Các webhook HTTP bên ngoài cho phép hệ thống khác kích hoạt công việc trong Moltbot. Xem [Webhooks](../automation/webhook.vi.md).

## Các Hook đi kèm sẵn có

Moltbot đi kèm với bốn Hook mặc định:

- **💾 session-memory**: Lưu bối cảnh phiên làm việc vào không gian làm việc của Agent khi bạn dùng lệnh `/new`.
- **📝 command-logger**: Ghi nhật ký tất cả các lệnh vào tệp `~/.clawdbot/logs/commands.log`.
- **🚀 boot-md**: Chạy tệp `BOOT.md` khi Gateway khởi động.
- **😈 soul-evil**: Thay đổi nội dung của `SOUL.md` một cách ngẫu nhiên hoặc theo khung giờ định sẵn.

## Bắt đầu sử dụng

Liệt kê các Hook hiện có:
```bash
moltbot hooks list
```

Bật một Hook:
```bash
moltbot hooks enable session-memory
```

Xem thông tin chi tiết:
```bash
moltbot hooks info session-memory
```

## Cách Moltbot tìm kiếm Hook

Hệ thống quét theo thứ tự ưu tiên:
1. **Workspace hooks**: `<workspace>/hooks/` (Dành riêng cho từng Agent, ưu tiên cao nhất).
2. **Managed hooks**: `~/.clawdbot/hooks/` (Người dùng cài đặt, dùng chung cho các không gian làm việc).
3. **Bundled hooks**: Đi kèm theo bộ cài Moltbot.

## Cấu trúc của một Hook

Mỗi Hook là một thư mục bao gồm:
- `HOOK.md`: Chứa siêu dữ liệu (metadata) và tài liệu hướng dẫn.
- `handler.ts`: Mã nguồn xử lý sự kiện.

## Các loại sự kiện hỗ trợ

### Sự kiện lệnh (Command Events)
Kích hoạt khi có lệnh gửi tới Agent:
- `command:new`: Khi dùng lệnh `/new`.
- `command:reset`: Khi dùng lệnh `/reset`.
- `command:stop`: Khi dùng lệnh `/stop`.

### Sự kiện Gateway
Kích hoạt khi Gateway khởi động:
- `gateway:startup`: Sau khi các kênh được khởi kiện và các hook được tải xong.

---
Tài liệu liên quan: [Plugin](../plugin.vi.md), [Cấu hình Gateway](../../gateway/configuration.vi.md).
