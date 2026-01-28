---
summary: "Hướng dẫn sử dụng công cụ thực thi lệnh, các chế độ đầu vào và hỗ trợ TTY"
read_when:
  - Bạn muốn cho phép AI chạy các lệnh Shell trong terminal
---
# Công cụ thực thi lệnh (`exec`)

Công cụ này cho phép AI chạy các lệnh Shell trực tiếp trong không gian làm việc. Nó hỗ trợ cả việc chạy ở chế độ chờ (đồng bộ) hoặc chạy ngầm (background).

## Các thông số chính
- `command` (bắt buộc): Lệnh bạn muốn chạy.
- `workdir`: Thư mục làm việc (mặc định là thư mục hiện tại).
- `background`: Chạy lệnh ngay lập tức ở chế độ ngầm (AI sẽ không phải đợi lệnh chạy xong mới trả lời tin nhắn khác).
- `timeout`: Thời gian tối đa cho phép lệnh chạy (để tránh các lệnh bị treo vĩnh viễn).
- `pty`: Chạy trong một thiết bị đầu cuối giả (cần thiết cho các lệnh yêu cầu giao diện văn bản như `htop`, `vim`).
- `host`: Nơi thực thi lệnh (`sandbox` - môi trường cô lập, `gateway` - máy chủ trung tâm, hoặc `node` - một máy tính khác được kết nối).

## Cấu hình PATH
Bạn có thể chỉ định các thư mục ưu tiên để AI tìm thấy các câu lệnh của bạn thông qua thiết lập `tools.exec.pathPrepend`.

## Các lệnh an toàn (`safeBins`)
Moltbot có một danh sách mặc định các câu lệnh được coi là "an toàn" vì chúng chỉ thao tác trên luồng văn bản và không gây nguy hiểm trực tiếp cho hệ thống (ví dụ: `jq`, `grep`, `sort`, `wc`). Các lệnh này có thể chạy mà không cần phê duyệt thủ công nếu bạn đã cấu hình đúng.

## Ví dụ sử dụng cho Agent
- Chạy lệnh đơn giản: `{"tool":"exec","command":"ls -la"}`
- Chạy lệnh ngầm và theo dõi: `{"tool":"exec","command":"npm run build","background": true}`

---
Tài liệu liên quan: [Phê duyệt thực thi lệnh](./exec-approvals.vi.md), [Chế độ đặc quyền](./elevated.vi.md), [Công cụ Patch](./apply-patch.vi.md).
