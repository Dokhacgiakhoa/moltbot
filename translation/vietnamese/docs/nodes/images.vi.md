---
summary: "Các quy tắc xử lý hình ảnh và đa phương tiện khi gửi tin và phản hồi của Bot"
read_when:
  - Bạn muốn gửi kèm hình ảnh, video khi Bot nhắn tin
---

# Hỗ trợ Hình ảnh & Đa phương tiện

Tài liệu này mô tả các quy tắc xử lý hình ảnh, âm thanh và video của Moltbot trên các kênh nhắn tin (như WhatsApp).

## Mục tiêu
- Gửi kèm hình ảnh/video khi nhắn tin qua lệnh: `moltbot message send --media`.
- Cho phép Bot tự động phản hồi bằng hình ảnh kèm nội dung văn bản.
- Duy trì giới hạn dung lượng hợp lý cho từng loại tệp.

## Hành vi trên kênh WhatsApp
- **Hình ảnh**: Tự động thay đổi kích thước và nén về định dạng JPEG (cạnh lớn nhất 2048px), dung lượng tối đa 5-6 MB.
- **m thanh/Video**: Hỗ trợ tệp lên đến 16 MB. m thanh được gửi dưới dạng tin nhắn thoại (Voice note).
- **Tài liệu**: Các loại tệp khác được hỗ trợ lên đến 100 MB.
- **Ảnh động (GIF)**: Được gửi dưới dạng video MP4 tự động lặp (loop).

## Xử lý đa phương tiện đầu vào
Khi bạn gửi một hình ảnh hoặc âm thanh cho Bot:
1. Bot sẽ tải tệp đó về một thư mục tạm.
2. Nếu được cấu hình, Bot sẽ sử dụng AI để "nhìn" ảnh hoặc "nghe" âm thanh để hiểu nội dung trước khi trả lời.
3. Các thông tin này sẽ được chèn vào ngữ cảnh của Bot dưới dạng `[Image]`, `[Audio]` (kèm văn bản chuyển đổi).
4. Bạn có thể truy cập đường dẫn tệp này thông qua biến `{{MediaPath}}` trong các tập lệnh (scripts).

## Giới hạn & Lỗi
- Nếu tệp quá lớn hoặc không đọc được, Bot sẽ ghi nhận lỗi và bỏ qua việc gửi/xử lý tệp đó.
- Giới hạn mặc định khi Bot "đọc" ảnh là 10 MB, âm thanh là 20 MB và video là 50 MB.

---
Tài liệu liên quan: [m thanh và tin nhắn thoại](./audio.vi.md), [Gửi tin nhắn qua CLI](../../cli/message.vi.md).
