---
summary: "Củng cố danh sách cho phép (allowlist) của Telegram: Chuẩn hóa tiền tố và khoảng trắng"
read_when:
  - Xem lại các thay đổi lịch sử về danh sách cho phép của Telegram
---

# Củng cố Danh sách cho phép Telegram

**Ngày**: 05-01-2026  
**Trạng thái**: Hoàn thành  

## Tóm tắt
Danh sách cho phép của Telegram (Allowlist) hiện đã chấp nhận các tiền tố `telegram:` và `tg:` (không phân biệt chữ hoa chữ thường) và tự động loại bỏ các khoảng trắng thừa. Điều này giúp việc kiểm tra tin nhắn đến đồng nhất với việc gửi tin nhắn đi.

## Những thay đổi chính
- Các tiền tố `telegram:` và `tg:` được coi là như nhau.
- Các mục nhập trong danh sách sẽ được tự động xóa khoảng trắng ở đầu và cuối; các mục trống sẽ bị bỏ qua.

## Ví dụ
Tất cả các định dạng sau hiện đều được chấp nhận cho cùng một ID:
- `telegram:123456`
- `TG:123456`
- ` tg:123456 `

## Tại sao điều này lại quan trọng?
Việc sao chép/dán ID từ nhật ký lỗi hoặc từ ứng dụng chat thường kéo theo cả tiền tố và khoảng trắng rác. Việc chuẩn hóa giúp hệ thống nhận diện chính xác người dùng để quyết định xem có nên trả lời tin nhắn trong nhóm hay tin nhắn riêng hay không.

---
Tài liệu liên quan: [Trò chuyện nhóm](../../concepts/groups.vi.md), [Nhà cung cấp Telegram](../../channels/telegram.vi.md).
