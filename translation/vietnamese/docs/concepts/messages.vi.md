---
summary: "Luồng tin nhắn, phiên làm việc, xếp hàng và hiển thị suy luận"
read_when:
  - Bạn muốn giải thích cách các tin nhắn đến trở thành phản hồi của Agent
  - Bạn cần làm rõ về phiên làm việc, chế độ hàng đợi hoặc hành vi truyền tin
---

# Tin nhắn (Messages)

Trang này tổng hợp cách Moltbot xử lý các tin nhắn đến, quản lý phiên làm việc, hàng đợi, truyền dữ liệu (streaming) và hiển thị quá trình suy luận của AI.

## Luồng tin nhắn (Cấp độ cao)

```
Tin nhắn đến
  -> Định tuyến/Ghép nối -> Khóa phiên làm việc
  -> Hàng đợi (nếu đang có lượt chạy khác)
  -> Lượt chạy Agent (Truyền tin + Công cụ)
  -> Phản hồi đầu ra (Giới hạn kênh + Cắt nhỏ tin nhắn)
```

Các cài đặt quan trọng nằm trong cấu hình:
- `messages.*`: Cài đặt tiền tố, hàng đợi và hành vi trong nhóm.
- `agents.defaults.*`: Cài đặt mặc định cho việc truyền tin theo khối và cắt nhỏ tin nhắn.

## Chống trùng lặp tin nhắn đến

Các kênh chat có thể gửi lại cùng một tin nhắn khi kết nối lại. Moltbot duy trì một bộ nhớ đệm ngắn hạn dựa trên ID tin nhắn để đảm bảo mỗi tin nhắn chỉ kích hoạt Agent một lần duy nhất.

## Gộp tin nhắn (Debouncing)

Khi bạn gửi nhiều tin nhắn liên tiếp một cách nhanh chóng, Moltbot có thể gộp chúng lại thành một lượt chạy duy nhất để tiết kiệm tài nguyên và trả lời mạch lạc hơn. Bạn có thể điều chỉnh thời gian chờ gộp bằng tham số `debounceMs`.

## Phiên làm việc và Thiết bị

Phiên làm việc thuộc quyền quản lý của Gateway, không phụ thuộc vào ứng dụng khách (client).
- Chat cá nhân sẽ được gộp vào phiên làm việc chính (`main`) của Agent.
- Các nhóm và kênh chat sẽ có các khóa phiên làm việc riêng biệt.
- Lịch sử chat và dữ liệu phiên được lưu trữ trực tiếp trên máy chủ chạy Gateway.

Khuyên dùng: Bạn nên sử dụng một thiết bị chính cho các cuộc hội thoại dài để tránh việc ngữ cảnh bị phân tán.

## Hiển thị suy luận (Reasoning)

Moltbot có thể hiển thị hoặc ẩn quá trình suy nghĩ của mô hình AI:
- Dùng lệnh `/reasoning on|off|stream` để điều khiển việc hiển thị.
- Nội dung suy nghĩ vẫn được tính vào số lượng Token tiêu thụ.
- Telegram hỗ trợ hiển thị luồng suy nghĩ ngay trong bóng bóng đang soạn thảo tin nhắn.

---
Tài liệu liên quan: [Cấu hình Gateway](../../gateway/configuration.vi.md), [Quản lý Phiên](./session.vi.md).
