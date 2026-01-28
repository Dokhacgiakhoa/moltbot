---
summary: "Cơ chế hoạt động bộ nhớ của Moltbot (tệp không gian làm việc + tự động đẩy dữ liệu bộ nhớ)"
read_when:
  - Bạn muốn tìm hiểu sơ đồ tệp bộ nhớ và quy trình làm việc
  - Bạn muốn điều chỉnh cơ chế đẩy dữ liệu trước khi nén ngữ cảnh
---

# Bộ nhớ (Memory)

Bộ nhớ của Moltbot là **các tệp Markdown thuần túy nằm trong không gian làm việc của Agent**. Các tệp này là nguồn dữ liệu gốc duy nhất; Agent chỉ "nhớ" những gì đã được ghi xuống đĩa cứng.

Các công cụ tìm kiếm bộ nhớ được cung cấp bởi plugin bộ nhớ mặc định (`memory-core`).

## Các tệp bộ nhớ (Markdown)

Cấu trúc mặc định sử dụng hai lớp bộ nhớ:

- **`memory/YYYY-MM-DD.md`**: Nhật ký hàng ngày (chỉ ghi thêm). Agent sẽ đọc báo cáo hôm nay và hôm qua khi bắt đầu phiên làm việc.
- **`MEMORY.md`**: (Tùy chọn) Bộ nhớ dài hạn được chọn lọc kỹ lưỡng. **Tệp này chỉ được nạp trong các phiên làm việc cá nhân, riêng tư** (không bao giờ nạp trong các nhóm chat).

Các tệp này nằm trong không gian làm việc (`agents.defaults.workspace`).

## Khi nào cần ghi vào bộ nhớ?

- Các quyết định, sở thích và sự thật quan trọng nên đưa vào `MEMORY.md`.
- Các ghi chú hàng ngày và ngữ cảnh đang thực hiện nên đưa vào `memory/YYYY-MM-DD.md`.
- Nếu bạn muốn Agent nhớ điều gì đó lâu dài, hãy **yêu cầu nó ghi lại** vào bộ nhớ thay vì chỉ nói suông.

## Tự động đẩy dữ liệu bộ nhớ (Memory Flush)

Khi một phiên làm việc **sắp đạt đến giới hạn nén ngữ cảnh**, Moltbot sẽ kích hoạt một **lượt chạy ngầm**. Lượt chạy này nhắc nhở Agent ghi lại các thông tin quan trọng vào bộ nhớ **trước khi** lịch sử chat bị nén lại.

Cơ chế này được điều khiển bởi tham số `agents.defaults.compaction.memoryFlush`. Thường thì lượt chạy này sẽ diễn ra âm thầm và người dùng sẽ không nhìn thấy bất kỳ phản hồi nào trong ô chat.

## Tìm kiếm bộ nhớ bằng Vector

Moltbot có thể xây dựng một chỉ mục vector nhỏ dựa trên các tệp `.md` trong bộ nhớ để thực hiện tìm kiếm ngữ nghĩa, giúp tìm thấy thông tin ngay cả khi cách dùng từ khác nhau.

- Mặc định tính năng này được bật.
- Hệ thống sẽ theo dõi sự thay đổi của các tệp bộ nhớ để cập nhật chỉ mục.
- Sử dụng nhà cung cấp dịch vụ nhúng (embeddings) như OpenAI hoặc Gemini để xử lý dữ liệu.

## Tìm kiếm hỗn hợp (Hybrid Search)

Moltbot kết hợp hai cơ chế tìm kiếm để đạt hiệu quả cao nhất:
- **Vector similarity**: Tìm kiếm theo ý nghĩa (ví dụ: "máy chủ" và "server" được coi là giống nhau).
- **BM25 keyword relevance**: Tìm kiếm chính xác theo từ khóa (ví dụ: số ID, tên biến, ký hiệu mã nguồn).

Sự kết hợp này giúp bạn tìm kiếm chính xác "cây kim trong đống cỏ" khi cần thông tin cụ thể (như mã lỗi), đồng thời vẫn hiểu được các câu hỏi bằng ngôn ngữ tự nhiên.

---
Tài liệu liên quan: [Không gian làm việc của Agent](./agent-workspace.vi.md), [Nén ngữ cảnh](./compaction.vi.md).
