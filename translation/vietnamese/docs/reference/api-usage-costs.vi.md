---
summary: "Kiểm tra các tính năng có thể gây tốn phí, các loại khóa API được sử dụng và cách xem mức độ sử dụng"
read_when:
  - Bạn muốn biết tính năng nào của Bot yêu cầu trả phí cho bên thứ ba
  - Bạn cần quản lý chi phí và hạn mức sử dụng API
---

# Sử dụng API & Chi phí

Tài liệu này liệt kê các **tính năng có thể tiêu tốn phí API** và nơi bạn có thể theo dõi các chi phí này.

## Nơi hiển thị chi phí (Chat + CLI)

- **Tóm tắt chi phí theo phiên**: Lệnh `/status` hiển thị mô hình đang dùng, mức độ sử dụng ngữ cảnh và **ước tính chi phí** cho câu trả lời gần nhất.
- **Báo cáo chi tiết**: Lệnh `/usage full` sẽ đính kèm thông tin sử dụng vào cuối mỗi câu trả lời của Bot.
- **Hạn mức nhà cung cấp**: Lệnh `moltbot status --usage` hiển thị biểu đồ sử dụng dựa trên hạn mức (quota) của nhà cung cấp.

## Các tính năng gây tốn phí

### 1) Phản hồi của mô hình cốt lõi
Đây là nguồn chi phí chính. Mỗi khi Bot trả lời hoặc sử dụng công cụ, nó sẽ gọi tới các nhà cung cấp như OpenAI, Anthropic, v.v.

### 2) Hiểu phương tiện truyền thông (Hình ảnh/Âm thanh/Video)
- **Âm thanh**: Sử dụng API OpenAI/Groq để chuyển từ giọng nói sang văn bản.
- **Hình ảnh/Video**: Sử dụng các mô hình có khả năng thị giác (Vision) để phân tích nội dung.

### 3) Tìm kiếm trí nhớ (Embeddings)
Nếu bạn cấu hình tìm kiếm trí nhớ bằng OpenAI hoặc Gemini (`memorySearch.provider`), mỗi khi Bot lưu hoặc tìm lại ký ức, nó sẽ tốn một khoản phí nhỏ cho việc tạo vector (embeddings).

### 4) Công cụ tìm kiếm Web
- **Brave Search**: Yêu cầu API Key. Có gói miễn phí 2.000 yêu cầu/tháng.
- **Perplexity**: Tính phí dựa trên số lượng câu hỏi tìm kiếm.

### 5) Đọc nội dung Web (Firecrawl)
Nếu bạn sử dụng Firecrawl để đọc các trang web phức tạp, nó sẽ tiêu tốn hạn mức của dịch vụ này.

### 6) Chuyển văn bản thành giọng nói (Talk)
Nếu cấu hình sử dụng **ElevenLabs**, bạn sẽ bị tính phí dựa trên số lượng ký tự mà Bot phát âm.

---
Tài liệu liên quan: [Các mô hình AI](../providers/models.vi.md), [Quản lý Trí nhớ](../concepts/memory.vi.md).
