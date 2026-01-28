---
summary: "Tham chiếu: Các quy tắc làm sạch và sửa chữa lịch sử hội thoại cho từng nhà cung cấp AI"
read_when:
  - AI từ chối trả lời do định dạng tin nhắn không hợp lệ
  - Bạn đang điều chỉnh logic xử lý các lần gọi công cụ (tool calls)
---

# "Vệ sinh" Hội thoại (Làm sạch dữ liệu cho AI)

Tài liệu này mô tả các **bản sửa lỗi đặc thù cho từng nhà cung cấp** được áp dụng vào lịch sử hội thoại ngay trước khi gửi tới AI. Các thay đổi này chỉ diễn ra **trong bộ nhớ tạm** để thỏa mãn yêu cầu khắt khe của từng loại mô hình, và sẽ **không** làm thay đổi nội dung tệp hội thoại gốc lưu trên ổ cứng.

## Tại sao cần làm việc này?
Mỗi nhà cung cấp AI (Google, Anthropic, OpenAI) có những quy tắc rất khác nhau về cách xâu chuỗi tin nhắn:
- **Google Gemini**: Yêu cầu xen kẽ nghiêm ngặt giữa người dùng và trợ lý. Nếu lịch sử bắt đầu bằng lời của trợ lý, Bot sẽ tự thêm một câu chào nhỏ của người dùng vào đầu.
- **Anthropic (Claude)**: Yêu cầu gộp các tin nhắn liên tiếp của cùng một người thành một khối duy nhất.
- **Mã định danh công cụ (Tool call ID)**: Một số mô hình chỉ chấp nhận mã số, một số chấp nhận cả chữ cái, và một số giới hạn độ dài đúng 9 ký tự.

## Các quy tắc chung
- **Làm sạch hình ảnh**: Tự động giảm kích thước hoặc nén lại các ảnh quá lớn để tránh bị nhà cung cấp từ chối vì quá dung lượng.
- **Xử lý suy nghĩ (Thought signatures)**: Loại bỏ các đoạn văn bản "suy nghĩ ngầm" của AI nếu chúng không được ký tên hợp lệ hoặc có định dạng không đúng.

## Trạng thái hiện tại
Kể từ phiên bản `2026.1.22`, toàn bộ logic làm sạch dữ liệu đã được tập trung vào bộ máy chạy AI (Embedded Runner). Riêng đối với **OpenAI**, chúng tôi áp dụng nguyên tắc "không can thiệp" trừ việc xử lý hình ảnh để đảm bảo tính nguyên bản tối đa của phản hồi.

---
Tài liệu liên quan: [Quản lý Phiên](./session-management-compaction.vi.md), [Nhà cung cấp Mô hình](../providers/models.vi.md).
