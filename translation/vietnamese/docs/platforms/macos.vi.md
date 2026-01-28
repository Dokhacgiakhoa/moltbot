---
summary: "Ứng dụng đi kèm Moltbot cho macOS (thanh menu + trình quản lý Gateway)"
read_when:
  - Bạn đang cài đặt ứng dụng Moltbot trên máy Mac
  - Bạn muốn hiểu cách ứng dụng Mac quản lý quyền hạn và dịch vụ hệ thống
---

# Ứng dụng Moltbot cho macOS (Thanh menu + Quản lý Gateway)

Ứng dụng macOS là **trợ lý trên thanh menu** cho Moltbot. Nó quản lý các quyền hạn hệ thống, điều khiển dịch vụ Gateway tại địa phương (qua launchd) và cung cấp các khả năng đặc thù của máy Mac cho Agent.

## Tính năng chính

- Hiển thị thông báo hệ thống và trạng thái trên thanh menu.
- Quản lý các quyền hạn bảo mật (TCC) như: Thông báo, Trợ năng, Ghi màn hình, Micro, Nhận dạng giọng nói và AppleScript.
- Chạy hoặc kết nối tới Gateway (cục bộ hoặc từ xa).
- Cung cấp các công cụ chỉ có trên macOS cho Agent: Canvas (Bảng vẽ), Camera, Ghi màn hình, và thực thi lệnh hệ thống (`system.run`).
- Tự động cài đặt CLI toàn cục (`moltbot`) khi được yêu cầu.

## Chế độ Cục bộ vs Từ xa

- **Cục bộ (Mặc định)**: Ứng dụng sẽ kết nối với một Gateway đang chạy trên máy Mac của bạn. Nếu chưa có, nó sẽ tự khởi động dịch vụ qua launchd.
- **Từ xa**: Ứng dụng kết nối tới một Gateway ở máy khác (qua SSH/Tailscale). Ở chế độ này, máy Mac của bạn sẽ đóng vai trò là một **Nút mạng (Node)** để Gateway từ xa có thể điều khiển các tính năng của máy Mac.

## Quản lý dịch vụ (Launchd)

Ứng dụng quản lý một dịch vụ chạy ngầm mang tên `bot.molt.gateway`. Bạn có thể điều khiển dịch vụ này qua Terminal:

```bash
# Khởi động lại dịch vụ
launchctl kickstart -k gui/$UID/bot.molt.gateway

# Dừng dịch vụ
launchctl bootout gui/$UID/bot.molt.gateway
```

## Các lệnh điều khiển hệ thống (`system.run`)

Tính năng `system.run` cho phép AI chạy các lệnh máy tính của bạn. Để đảm bảo an toàn, bạn có thể kiểm soát danh sách các lệnh được phép trong phần **Settings → Exec approvals** của ứng dụng.

- **Danh sách trắng (Allowlist)**: Bạn có thể chỉ định chính xác những tệp thực thi nào AI được phép dùng.
- **Xác nhận (Ask)**: Ứng dụng sẽ hiện thông báo hỏi ý kiến bạn trước khi AI chạy một lệnh lạ.

## Quy trình thiết lập điển hình

1. Tải và mở **Moltbot.app**.
2. Hoàn thành bảng kiểm quyền hạn (nhấn cho phép các thông báo của hệ thống).
3. Đảm bảo chế độ **Local** đang bật và Gateway đã sẵn sàng.
4. Cài đặt thêm CLI nếu bạn muốn sử dụng Bot từ Terminal.

---
Tài liệu liên quan: [Quyền hạn trên macOS](./mac/permissions.vi.md), [Vận hành Gateway](../../gateway/index.vi.md).
