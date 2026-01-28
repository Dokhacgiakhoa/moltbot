---
summary: "Từ khóa đánh thức giọng nói toàn cầu và cách đồng bộ hóa giữa các thiết bị"
read_when:
  - Bạn muốn thay đổi từ khóa để gọi Bot (ví dụ: thay đổi từ 'Clawd' thành 'Bot ơi')
---

# Đánh thức bằng giọng nói (Voice Wake)

Moltbot quản lý **danh sách từ khóa đánh thức duy nhất** được lưu trữ tại **Gateway**.

- **Không có từ khóa riêng cho từng thiết bị**: Mọi thiết bị kết nối sẽ dùng chung một danh sách từ khóa.
- **Đồng bộ hóa tức thì**: Bất kỳ thiết bị hoặc ứng dụng nào thay đổi danh sách từ khóa, sự thay đổi đó sẽ được Gateway lưu lại và phát sóng đến tất cả các thiết bị khác đang kết nối.
- Mỗi thiết bị vẫn có nút **Bật/Tắt** riêng để người dùng quyết định xem có muốn thiết bị đó luôn lắng nghe hay không.

## Lưu trữ (Tại Gateway)
Từ khóa được lưu tại:
`~/.clawdbot/settings/voicewake.json`

Định dạng mẫu:
```json
{ "triggers": ["clawd", "claude", "computer"] }
```

## Cách hoạt động của ứng dụng
### Ứng dụng macOS
- Sử dụng danh sách này để kích hoạt Bot khi bạn gọi tên nó.
- Khi bạn sửa "Từ khóa kích hoạt" trong cài đặt, ứng dụng sẽ gửi lệnh cập nhật lên Gateway để đồng bộ với điện thoại của bạn.

### Nút iOS/Android (Điện thoại)
- Tự động nhận danh sách từ khóa mới nhất từ Gateway ngay khi kết nối.
- Bạn có thể sửa từ khóa trực tiếp trên điện thoại, và máy tính ở nhà cũng sẽ được cập nhật theo.

## Lưu ý
- Các từ khóa sẽ được chuẩn hóa (xóa khoảng trắng thừa, chuyển về chữ thường).
- Nếu danh sách trống, hệ thống sẽ sử dụng các từ khóa mặc định.
- Để tính năng này hoạt động, bạn cần cấp quyền truy cập Microphone cho ứng dụng trên từng thiết bị.

---
Tài liệu liên quan: [Chế độ Trò chuyện](./talk.vi.md), [Các nút mạng (Nodes)](./index.vi.md).
