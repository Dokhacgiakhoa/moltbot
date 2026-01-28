---
summary: "Giao thức cầu nối (Dành cho thiết bị đời cũ): Cấu trúc, xác thực và các lệnh RPC"
read_when:
  - Bạn đang nghiên cứu về các phiên bản Moltbot cũ hoặc gỡ lỗi các thiết bị chưa nâng cấp lên WebSocket
---

# Giao thức cầu nối (Bridge protocol)

Giao thức Cầu nối là một phương thức truyền tải dữ liệu **đời cũ (legacy)** dựa trên TCP. Hiện nay, tất cả các thiết bị mới nên sử dụng giao thức **Gateway WebSocket** thống nhất.

**Lưu ý quan trọng**: Các phiên bản Moltbot hiện tại không còn kích hoạt bộ lắng nghe TCP Bridge theo mặc định. Tài liệu này được giữ lại với mục đích tham khảo lịch sử.

## Tại sao giao thức này từng tồn tại?

- **Ranh giới bảo mật**: Cầu nối chỉ cho phép một danh sách các hành động giới hạn thay vì toàn bộ API của Gateway.
- **Định danh thiết bị**: Việc tiếp nhận thiết bị do Gateway quản lý và gắn liền với một Token riêng cho từng Node.
- **Tiện ích khám phá**: Cho phép các thiết bị cũ tìm thấy Gateway qua Bonjour trong mạng LAN.

## Quy trình bắt tay và ghép nối

1. Thiết bị gửi lệnh `hello` kèm theo thông tin phần cứng và Token (nếu đã từng ghép nối).
2. Nếu chưa được ghép nối, Gateway trả về lỗi `NOT_PAIRED`.
3. Thiết bị gửi yêu cầu `pair-request`.
4. Gateway chờ chủ sở hữu phê duyệt trên Terminal, sau đó gửi `pair-ok`.

---
Tài liệu liên quan: [Giao thức Gateway hiện đại](./protocol.vi.md), [Ghép nối thiết bị](./pairing.vi.md).
