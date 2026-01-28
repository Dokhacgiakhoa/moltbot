---
summary: "Cửa sổ ngữ cảnh và Nén ngữ cảnh: Cách Moltbot giữ cho các phiên làm việc luôn nằm trong giới hạn của mô hình AI"
read_when:
  - Bạn muốn tìm hiểu về cơ chế nén tự động và lệnh /compact
  - Bạn đang gặp lỗi về giới hạn ngữ cảnh khi trò chuyện quá dài
---

# Cửa sổ ngữ cảnh & Nén ngữ cảnh

Mỗi mô hình AI đều có một **cửa sổ ngữ cảnh** (số lượng Token tối đa mà nó có thể "nhìn thấy" cùng một lúc). Các cuộc trò chuyện kéo dài sẽ tích lũy tin nhắn và kết quả của công cụ; khi cửa sổ này bị lấp đầy, Moltbot sẽ thực hiện **nén ngữ cảnh (compaction)** các tin nhắn cũ để nhường chỗ cho dữ liệu mới.

## Nén ngữ cảnh là gì?
Cơ chế này sẽ **tóm tắt toàn bộ lịch sử trò chuyện cũ** thành một mục tóm tắt ngắn gọn và giữ nguyên các tin nhắn gần đây. Bản tóm tắt này được lưu trực tiếp vào lịch sử phiên làm việc (JSONL), nên các yêu cầu sau này sẽ sử dụng:
- Bản tóm tắt ngữ cảnh.
- Các tin nhắn mới sau thời điểm nén.

## Nén tự động (Mặc định bật)
Khi một phiên làm việc sắp đạt đến giới hạn của mô hình, Moltbot sẽ tự động thực hiện nén và thử lại yêu cầu của bạn bằng ngữ cảnh đã được tinh gọn.

Bạn sẽ thấy thông báo:
- `🧹 Auto-compaction complete` (trong chế độ hiển thị chi tiết - verbose).
- Lệnh `/status` sẽ hiển thị `🧹 Compactions: <số lần>`.

Trước khi nén, Moltbot có thể thực hiện một lượt **đẩy dữ liệu vào bộ nhớ (memory flush)** để lưu các thông tin quan trọng vào đĩa cứng. Xem thêm tại [Bộ nhớ Agent](./memory.vi.md).

## Nén thủ công
Bạn có thể gõ lệnh `/compact` (có kèm theo chỉ dẫn nếu muốn) để ép buộc hệ thống thực hiện nén ngay lập tức:
```
/compact Hãy tập trung vào các quyết định quan trọng và những câu hỏi chưa có lời giải.
```

## Phân biệt Nén và Cắt tỉa (Pruning)
- **Nén (Compaction)**: Tóm tắt nội dung và **lưu vĩnh viễn** vào lịch sử chat.
- **Cắt tỉa (Session pruning)**: Chỉ tạm thời xóa bớt các **kết quả của công cụ** quá dài ra khỏi bộ nhớ trong lúc chạy (không lưu đè lên lịch sử).

Xem chi tiết tại [Cắt tỉa phiên làm việc](./session-pruning.vi.md).

---
Tài liệu liên quan: [Ngữ cảnh (Context)](./context.vi.md), [Xử lý phiên làm việc](./session.vi.md).
