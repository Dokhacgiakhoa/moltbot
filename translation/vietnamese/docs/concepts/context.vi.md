---
summary: "Ngữ cảnh: Những gì mô hình AI nhìn thấy, cách nó được xây dựng và cách kiểm tra thông tin"
read_when:
  - Bạn muốn hiểu rõ khái niệm “ngữ cảnh” trong Moltbot
  - Bạn đang gỡ lỗi tại sao Agent nhớ (hoặc quên) một thông tin gì đó
  - Bạn muốn tối ưu hóa dung lượng ngữ cảnh để tiết kiệm chi phí
---

# Ngữ cảnh (Context)

“Ngữ cảnh” là **tất cả mọi thứ mà Moltbot gửi đến cho mô hình AI trong một lượt chạy**. Nó bị giới hạn bởi **cửa sổ ngữ cảnh** (giới hạn Token) của từng mô hình.

Cấu trúc cơ bản của ngữ cảnh:
- **Câu lệnh hệ thống (System prompt)**: Các quy tắc, danh sách công cụ, kỹ năng, thời gian và các tệp khởi tạo từ không gian làm việc.
- **Lịch sử trò chuyện**: Tin nhắn của bạn và phản hồi của Agent trong phiên làm việc này.
- **Kết quả gọi công cụ & Tệp đính kèm**: Kết quả thực thi lệnh, nội dung file đã đọc, hình ảnh/âm thanh, v.v.

Ngữ cảnh *không giống* với “bộ nhớ” (memory): bộ nhớ được lưu trên đĩa và có thể tải lại sau; còn ngữ cảnh là những gì nằm bên trong cửa sổ làm việc hiện tại của mô hình.

## Kiểm tra ngữ cảnh nhanh

- `/status`: Xem nhanh "cửa sổ ngữ cảnh đã đầy bao nhiêu?" và các cài đặt phiên.
- `/context list`: Xem danh sách các thành phần được nạp vào và kích thước ước tính của chúng.
- `/context detail`: Xem chi tiết sâu hơn về kích thước các schema công cụ, các kỹ năng và câu lệnh hệ thống.
- `/compact`: Tóm tắt lịch sử cũ để giải phóng không gian cho cửa sổ ngữ cảnh.

## Moltbot xây dựng câu lệnh hệ thống như thế nào?

Câu lệnh hệ thống do Moltbot quản lý và được xây dựng lại sau mỗi lần chạy. Nó bao gồm:
- Danh sách công cụ + mô tả ngắn.
- Danh sách kỹ năng (chỉ lấy mô tả).
- Vị trí không gian làm việc.
- Thời gian (giờ quốc tế + giờ địa phương của người dùng).
- Thông tin về hệ điều hành, máy chủ, mô hình AI.
- Các tệp khởi tạo quan trọng (`AGENTS.md`, `SOUL.md`, `USER.md`, `IDENTITY.md`, v.v.).

## Các tệp Ngữ cảnh Dự án

Mặc định, Moltbot sẽ nạp các tệp sau từ không gian làm việc của bạn:
- `AGENTS.md`: Chỉ dẫn vận hành Agent.
- `SOUL.md`: Tính cách và ranh giới hành vi.
- `TOOLS.md`: Các lưu ý về cách dùng công cụ.
- `IDENTITY.md`: Tên và biểu tượng của Agent.
- `USER.md`: Thông tin về chính bạn.
- `HEARTBEAT.md`: Chỉ dẫn cho các lượt chạy tự động.

Các tệp quá lớn sẽ bị cắt bớt dựa trên tham số `agents.defaults.bootstrapMaxChars` (mặc định là 20.000 ký tự). Bạn có thể dùng lệnh `/context` để biết tệp nào đang bị cắt bớt.

## Lệnh Slash và Chỉ dẫn (Directives)

Các lệnh bắt đầu bằng dấu `/` được Gateway xử lý trước khi gửi đến mô hình:
- **Lệnh độc lập**: Một tin nhắn chỉ có `/...` sẽ được thực thi như một lệnh hệ thống.
- **Chỉ dẫn (Directives)**: Các từ khóa như `/think`, `/verbose`, `/model` sẽ được Gateway lọc bỏ và áp dụng cài đặt tương ứng thay vì gửi cho mô hình xem. Bạn có thể dùng chúng độc lập hoặc chèn vào giữa tin nhắn để điều chỉnh hành vi cho riêng lượt chạy đó.

---
Tài liệu liên quan: [Lệnh Slash](../../tools/slash-commands.md), [Sử dụng Token](../../token-use.vi.md), [Nén ngữ cảnh](./compaction.vi.md).
