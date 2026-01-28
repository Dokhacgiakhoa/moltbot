---
summary: "Hành vi truyền tin và cắt nhỏ tin nhắn (trả lời theo khối, truyền tin nháp, giới hạn)"
read_when:
  - Bạn muốn tìm hiểu cách Agent gửi tin nhắn dần dần thay vì gửi một cục
---

# Truyền tin & Cắt nhỏ tin nhắn

Moltbot có hai lớp "truyền tin" (streaming) riêng biệt:
- **Truyền tin theo khối (Block streaming)**: Gửi các **đoạn văn bản hoàn chỉnh** ngay khi Agent vừa viết xong. Đây là các tin nhắn bình thường trên ứng dụng chat.
- **Truyền tin nháp (Chỉ dành cho Telegram)**: Cập nhật liên tục một **bong bóng tin nhắn nháp** trong khi AI đang suy nghĩ; tin nhắn chính thức chỉ được gửi khi đã hoàn thành.

## Truyền tin theo khối (Block streaming)

Cơ chế này gửi phản hồi của Agent theo từng đoạn lớn ngay khi có dữ liệu.

**Các tùy chọn điều khiển:**
- `blockStreamingDefault`: Bật hoặc tắt tính năng này (mặc định tắt).
- `blockStreamingBreak`: 
  - `text_end`: Gửi ngay khi có một đoạn văn bản nhỏ hoàn thành.
  - `message_end`: Đợi Agent viết xong toàn bộ rồi mới bắt đầu chia nhỏ để gửi.
- `humanDelay`: Thêm một khoảng thời gian tạm dừng ngẫu nhiên giữa các khối tin nhắn để tạo cảm giác giống như người đang gõ văn bản thật (mặc định tắt).

## Thuật toán cắt nhỏ tin nhắn
Khi Agent viết một đoạn văn quá dài vượt quá giới hạn của ứng dụng chat (ví dụ như WhatsApp hay Telegram), Moltbot sẽ tự động chia nhỏ nó:
- Ưu tiên ngắt ở các vị trí như: Hết đoạn văn -> Hết dòng -> Hết câu -> Khoảng trắng.
- **Khối mã nguồn (Code blocks)**: Không bao giờ bị ngắt ở giữa. Nếu buộc phải ngắt vì quá dài, hệ thống sẽ tự động đóng khối mã ở đoạn trước và mở lại ở đoạn sau để định dạng Markdown luôn hiển thị đúng.

## Truyền tin nháp trên Telegram
Telegram là nền tảng duy nhất hỗ trợ việc nhìn thấy AI đang "soạn thảo" một cách chi tiết:
- Agent sẽ cập nhật nội dung vào một bóng bóng nháp.
- Bạn có thể thấy cả quá trình suy nghĩ (reasoning) của AI ngay trong bong bóng này nếu bật lệnh `/reasoning stream`.
- Khi kết thúc, một tin nhắn chính thức sẽ được gửi và bóng bóng nháp sẽ biến mất.

---
Tài liệu liên quan: [Cấu hình Gateway](../../gateway/configuration.vi.md), [Hàng đợi lệnh](./queue.vi.md).
