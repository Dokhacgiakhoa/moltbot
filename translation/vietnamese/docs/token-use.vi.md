---
summary: "Cách Moltbot xây dựng bối cảnh (context) và báo cáo mức độ sử dụng Token + chi phí"
---

# Sử dụng Token & Chi phí

Moltbot theo dõi số lượng **Token**, không phải ký tự. Các Token mang tính đặc thù của từng mô hình, nhưng hầu hết các mô hình kiểu OpenAI tính trung bình khoảng 4 ký tự cho mỗi Token đối với văn bản tiếng Anh.

## Cách xây dựng Câu lệnh hệ thống (System Prompt)

Moltbot lắp ghép câu lệnh hệ thống của riêng mình cho mỗi lần chạy, bao gồm:
- Danh sách công cụ & mô tả ngắn.
- Danh sách các kỹ năng (chỉ chứa siêu dữ liệu; nội dung kỹ năng sẽ được tải khi cần).
- Hướng dẫn tự cập nhật.
- Các tệp tin bối cảnh của Agent (`AGENTS.md`, `SOUL.md`, `IDENTITY.md`, v.v.). Các tệp lớn sẽ bị cắt ngắn để tiết kiệm bối cảnh.
- Thời gian hiện tại.
- Dữ liệu về máy chủ, hệ điều hành và mô hình đang sử dụng.

## Những gì được tính vào Cửa sổ bối cảnh (Context Window)

Mọi dữ liệu mà mô hình nhận được đều tính vào giới hạn bối cảnh:
- Câu lệnh hệ thống (như trên).
- Lịch sử trò chuyện (tin nhắn của bạn và của Bot).
- Các lệnh gọi công cụ và kết quả của chúng.
- Các tệp đính kèm (hình ảnh, âm thanh, tệp tin).

Bạn có thể dùng lệnh `/context list` hoặc `/context detail` để xem bảng liệt kê chi tiết dung lượng của từng phần.

## Cách xem mức độ sử dụng Token hiện tại

Bạn có thể gõ các lệnh sau trong chat:
- `/status`: Hiển thị bảng trạng thái với thông tin bối cảnh đã dùng, số Token của phản hồi gần nhất và **chi phí ước tính** (nếu dùng API key).
- `/usage off|tokens|full`: Thêm phần chân trang (footer) về mức sử dụng vào cuối mỗi câu trả lời của Bot.
- `/usage cost`: Hiển thị bảng tổng hợp chi phí dựa trên nhật ký phiên làm việc.

## Ước tính chi phí

Chi phí được tính toán dựa trên mức giá bạn cấu hình trong mục `models.providers`. Giá này thường tính theo đơn vị **USD trên 1 triệu Token** cho các loại: đầu vào (input), đầu ra (output), đọc bộ nhớ đệm (cacheRead) và ghi bộ nhớ đệm (cacheWrite). 

*Lưu ý: Nếu bạn dùng các tài khoản OAuth (như Claude Pro/Plus), chi phí sẽ được ẩn vì bạn đã trả thuê bao cố định.*

## Mẹo để giảm thiểu việc sử dụng Token

- Sử dụng lệnh `/compact` để tóm tắt các phiên trò chuyện dài.
- Giữ mô tả các kỹ năng (skills) ngắn gọn và súc tích.
- Ưu tiên các mô hình nhỏ/rẻ cho các công việc mang tính thăm dò hoặc lặp lại nhiều lần.
- Sử dụng cơ chế **Nhịp tim (Heartbeat)** để giữ cho bộ nhớ đệm (cache) luôn "nóng", giúp giảm chi phí ghi bộ nhớ đệm (cache write) khi bối cảnh hầu như không thay đổi giữa các tin nhắn.

---
Tài liệu liên quan: [Cửa sổ bối cảnh](../concepts/context.vi.md), [Cấu hình hệ thống](../gateway/configuration.vi.md).
