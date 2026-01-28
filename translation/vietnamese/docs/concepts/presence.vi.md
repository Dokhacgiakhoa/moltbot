---
summary: "Trạng thái hiện diện trong Moltbot: Cách tạo, gộp và hiển thị danh sách hoạt động"
read_when:
  - Bạn muốn tìm hiểu về danh sách các tệp/thiết bị đang kết nối tới Gateway
---

# Trạng thái hiện diện (Presence)

Trạng thái hiện diện trong Moltbot là một cái nhìn tổng quan nhanh về:
- Chính bản thân **Gateway**.
- Các **ứng dụng khách (clients)** đang kết nối tới Gateway (ứng dụng Mac, WebChat, CLI, v.v.).

Thông tin này chủ yếu dùng để hiển thị trong tab **Instances** của ứng dụng macOS và giúp người quản trị biết ai đang truy cập hệ thống.

## Các thông tin hiển thị

Mỗi bản ghi trạng thái bao gồm các trường như:
- `instanceId`: Định danh cố định của thiết bị kết nối.
- `host`: Tên máy tính.
- `ip`: Địa chỉ IP của thiết bị.
- `version`: Phiên bản của ứng dụng khách.
- `mode`: Loại kết nối (ví dụ: `ui` - giao diện đồ họa, `cli` - dòng lệnh, `node` - thiết bị đầu cuối).
- `reason`: Lý do ghi nhận trạng thái (kết nối mới, cập nhật định kỳ).
- `ts`: Thời điểm cập nhật cuối cùng.

## Nguồn tạo trạng thái

1. **Bản thân Gateway**: Luôn tự tạo một mục "tôi đang chạy" khi khởi động.
2. **Khi kết nối WebSocket**: Mọi ứng dụng khi kết nối sẽ khai báo thông tin của mình.
   - *Lưu ý*: Các lệnh CLI ngắn gọn (chỉ chạy rồi tắt) thường sẽ không hiển thị để tránh làm rối danh sách.
3. **Tín hiệu đèn báo (system-event beacons)**: Các ứng dụng gửi thông tin cập nhật định kỳ (như thời gian người dùng không hoạt động).
4. **Kết nối của các Node**: Khi bạn ghép nối camera hay màn hình, chúng cũng xuất hiện trong danh sách này.

## Quy tắc xóa bỏ (TTL)

Trạng thái hiện diện chỉ mang tính chất tạm thời:
- Các mục không cập nhật trong vòng **5 phút** sẽ bị tự động xóa.
- Danh sách tối đa là **200 mục** (mục cũ nhất sẽ bị đẩy ra nếu danh sách đầy).

Điều này đảm bảo danh sách luôn mới và không chiếm dụng bộ nhớ hệ thống.

## Mẹo gỡ lỗi
Để xem danh sách thô của tất cả các thiết bị đang hiện diện, bạn có thể thực hiện yêu cầu `system-presence` tới Gateway.

---
Tài liệu liên quan: [Ghép nối thiết bị](../../start/pairing.vi.md), [Giao thức Gateway](../../gateway/protocol.vi.md).
