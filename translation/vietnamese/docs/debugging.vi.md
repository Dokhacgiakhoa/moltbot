---
summary: "Công cụ gỡ lỗi (Debugging): Chế độ theo dõi (watch mode), xem luồng dữ liệu thô từ mô hình và các lệnh /debug"
---

# Gỡ lỗi (Debugging)

Trang này giới thiệu các công cụ hỗ trợ gỡ lỗi, đặc biệt là khi bạn cần kiểm tra luồng dữ liệu thô từ các mô hình AI hoặc khi xử lý các phần suy luận (reasoning) bị trộn lẫn vào văn bản.

## Ghi đè cấu hình tạm thời (`/debug`)

Bạn có thể sử dụng lệnh `/debug` trực tiếp trong chat để thay đổi các cài đặt cấu hình **chỉ trong bộ nhớ tạm** (không lưu vào ổ đĩa). Tính năng này mặc định bị tắt; bạn có thể bật nó bằng cách đặt `commands.debug: true`.

Ví dụ:
- `/debug show`: Xem các cấu hình đang được ghi đè.
- `/debug set messages.responsePrefix="[moltbot]"`: Đặt tiền tố cho câu trả lời.
- `/debug reset`: Xóa bỏ toàn bộ các ghi đè và quay về cấu hình gốc trên ổ đĩa.

## Chế độ theo dõi Gateway (Watch mode)

Để phát triển và thử nghiệm nhanh, bạn có thể chạy Gateway ở chế độ theo dõi thay đổi tệp tin:

```bash
pnpm gateway:watch --force
```

Mỗi khi bạn thay đổi mã nguồn, Gateway sẽ tự động khởi động lại.

## Chế độ phát triển (`--dev`)

Sử dụng cờ `--dev` để cách ly dữ liệu và tạo ra một môi trường thử nghiệm an toàn, có thể xóa bỏ bất cứ lúc nào:
- Dữ liệu được lưu tại `~/.clawdbot-dev`.
- Cổng Gateway mặc định đổi thành `19001` (để không xung đột với bản chạy thật).
- Tự động tạo cấu hình và không gian làm việc tối giản nếu chưa có.
- Danh tính mặc định của Bot là **C3-PO**.

Để xóa sạch dữ liệu và bắt đầu lại từ đầu trong chế độ dev:
```bash
pnpm gateway:dev:reset
```

## Xem luồng dữ liệu thô (Raw stream logging)

Để kiểm tra xem mô hình AI thực sự gửi về cái gì (trước khi Moltbot lọc hay định dạng lại), bạn có thể bật ghi nhật ký luồng thô:

```bash
pnpm gateway:watch --force --raw-stream
```

Nhật ký sẽ được ghi vào tệp: `~/.clawdbot/logs/raw-stream.jsonl`.

## Lưu ý an toàn (Safety notes)

- Nhật ký luồng thô có thể chứa toàn bộ câu lệnh (prompts), kết quả công cụ và dữ liệu người dùng.
- Hãy chỉ lưu nhật ký tại máy cục bộ và xóa ngay sau khi gỡ lỗi xong.
- Nếu bạn chia sẻ nhật ký cho người khác, hãy xóa sạch các thông tin nhạy cảm và API key.

---
Tài liệu liên quan: [Nhật ký hệ thống](./logging.vi.md), [Xử lý sự cố](./help/troubleshooting.vi.md).
