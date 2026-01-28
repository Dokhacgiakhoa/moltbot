---
summary: "Cắt tỉa phiên làm việc: Thu gọn kết quả của công cụ để giảm dung lượng ngữ cảnh"
read_when:
  - Bạn muốn giảm tốc độ tăng trưởng ngữ cảnh AI do kết quả của các công cụ quá dài
---

# Cắt tỉa phiên làm việc (Session Pruning)

Cơ chế này giúp lược bỏ các **kết quả cũ của công cụ** ra khỏi bộ nhớ ngữ cảnh ngay trước mỗi lần gọi AI. Lưu ý rằng nó **không** ghi đè hay thay đổi lịch sử chat lưu trên đĩa cứng (`*.jsonl`).

## Tại sao cần cắt tỉa?
- **Tiết kiệm chi phí**: Giảm số lượng Token đầu vào gửi cho AI.
- **Tối ưu hóa bộ nhớ đệm (Cache)**: Anthropic có tính năng lưu bộ nhớ đệm (Prompt Caching). Nếu bạn để phiên làm việc quá tải với các kết quả công cụ cũ không còn dùng tới, nhà cung cấp sẽ phải nạp lại toàn bộ dữ liệu này sau một khoảng thời gian chờ (TTL), gây tốn kém không đáng có.

## Những gì sẽ bị cắt tỉa?
- Hệ thống chỉ tác động lên các tin nhắn loại `toolResult` (kết quả trả về từ các công cụ).
- Các tin nhắn của người dùng và phản hồi của Agent **không bao giờ** bị thay đổi.
- Agent luôn bảo vệ một số lượng nhất định các tin nhắn phản hồi gần nhất (`keepLastAssistants`).

## Cắt tỉa mềm và Cắt tỉa cứng

- **Cắt tỉa mềm (Soft-trim)**: Chỉ áp dụng cho các kết quả công cụ quá dài. Hệ thống sẽ giữ lại phần đầu và phần cuối, thay thế phần giữa bằng dấu `...` và ghi chú rõ kích thước gốc. Điều này giúp Agent vẫn biết sơ qua về nội dung mà không tốn quá nhiều dung lượng.
- **Cắt tỉa cứng (Hard-clear)**: Thay thế toàn bộ kết quả công cụ cũ bằng một dòng thông báo ngắn gọn: `[Nội dung kết quả công cụ cũ đã được xóa bỏ]`.

## Cấu hình
Mặc định tính năng này được bật cho các mô hình của Anthropic với các thông số tối ưu:

```json
{
  "agent": {
    "contextPruning": {
      "mode": "cache-ttl",
      "ttl": "5m",
      "keepLastAssistants": 3
    }
  }
}
```

---
Tài liệu liên quan: [Cửa sổ ngữ cảnh & Nén ngữ cảnh](./compaction.vi.md), [Ngữ cảnh AI](./context.vi.md).
