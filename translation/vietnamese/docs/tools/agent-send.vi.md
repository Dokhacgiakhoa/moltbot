---
summary: "Cách chạy lệnh `moltbot agent` trực tiếp từ CLI (có tùy chọn gửi phản hồi)"
read_when:
  - Bạn muốn chạy agent từ dòng lệnh mà không cần gửi tin nhắn từ ứng dụng chat
---
# `moltbot agent` (Chạy agent trực tiếp)

Lệnh `moltbot agent` cho phép bạn thực hiện một lượt xử lý của agent mà không cần nhận tin nhắn từ ứng dụng chat. Theo mặc định, lệnh này sẽ kết nối qua Gateway; bạn có thể dùng thêm cờ `--local` để buộc nó chạy bằng trình thực thi nhúng ngay trên máy hiện tại.

## Cách thức hoạt động
- **Yêu cầu bắt buộc**: Phải có cờ `--message "<nội dung>"` (tin nhắn đầu vào).
- **Lựa chọn phiên làm việc**:
  - Dùng `--to <đích>` để xác định phiên (tin nhắn trực tiếp sẽ gộp vào phiên chính, tin nhắn nhóm/kênh sẽ được cô lập).
  - Dùng `--session-id <id>` để tiếp tục một phiên hiện có.
  - Dùng `--agent <id>` để gọi trực tiếp một agent đã cấu hình.
- **Kết quả đầu ra**: Mặc định sẽ in ra văn bản phản hồi của agent. Dùng cờ `--json` để nhận dữ liệu có cấu trúc.
- **Gửi phản hồi ngược lại kênh**: Dùng cờ `--deliver --channel <tên_kênh>` để gửi câu trả lời của agent tới một ứng dụng chat cụ thể.

## Ví dụ
```bash
# Chạy agent ops để tóm tắt log
moltbot agent --agent ops --message "Tóm tắt các file log"

# Chạy agent và gửi kết quả tới số điện thoại WhatsApp
moltbot agent --to +8490xxxxxxx --message "Gửi báo cáo tình trạng" --deliver

# Tiếp tục một phiên hiện có với mức độ suy nghĩ cao
moltbot agent --session-id 1234 --message "Tiếp tục phân tích" --thinking high
```

## Các cờ (Flags) quan trọng
- `--local`: Chạy cục bộ (yêu cầu bạn đã nạp API key của mô hình vào môi trường shell).
- `--deliver`: Gửi phản hồi của agent tới kênh chat tương ứng.
- `--channel`: Kênh chat đích (`whatsapp|telegram|discord|googlechat|slack|signal|imessage`).
- `--thinking <mức_độ>`: Thiết lập mức độ suy nghĩ cho AI (off|low|medium|high).
- `--verbose <on|off>`: Bật/tắt chế độ hiển thị chi tiết quá trình chạy của agent.
- `--json`: Xuất kết quả dưới định dạng JSON.

---
Tài liệu liên quan: [Cấu hình Gateway](../../gateway/configuration.vi.md), [Quản lý phiên](../concepts/session.vi.md).
