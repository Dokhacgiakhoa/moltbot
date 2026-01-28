---
summary: "Khi nào Moltbot hiển thị chỉ báo đang nhập tin nhắn và cách tùy chỉnh"
read_when:
  - Thay đổi hành vi hoặc thiết lập mặc định của các chỉ báo đang nhập
---
# Chỉ báo đang nhập (Typing indicators)

Các chỉ báo "đang nhập tin nhắn" được gửi tới kênh chat khi agent đang tích cực xử lý. 

## Các chế độ hoạt động
Bạn có thể cấu hình `agents.defaults.typingMode` với các giá trị:
- `never`: Không bao giờ hiển thị.
- `instant`: Hiển thị **ngay khi lượt chạy của agent bắt đầu**, kể cả khi sau đó bot không có gì để nói.
- `thinking`: Chỉ bắt đầu hiển thị khi AI **bắt đầu quá trình suy luận** (yêu cầu bật `/reasoning stream`).
- `message`: Chỉ hiển thị khi AI **bắt đầu tạo nội dung tin nhắn thực tế** (bỏ qua các phản hồi im lặng).

Thứ tự kích hoạt từ trễ đến sớm:
`never` → `message` → `thinking` → `instant`

## Cấu hình
```json5
{
  agent: {
    typingMode: "thinking",
    typingIntervalSeconds: 6
  }
}
```
Thông số `typingIntervalSeconds` kiểm soát **tần suất làm mới** (nhắc lại) trạng thái đang nhập để đảm bảo ứng dụng chat không tự động tắt nó đi (mặc định là 6 giây).

## Lưu ý
- Chế độ `message` sẽ giúp bot trông "lịch sự" hơn vì nó không hiện đang nhập nếu nó quyết định im lặng.
- Các lượt chạy nhịp đập (heartbeats) sẽ không bao giờ hiển thị trạng thái đang nhập để tránh làm phiền người dùng.

---
Tài liệu liên quan: [Tin nhắn](./messages.vi.md).
