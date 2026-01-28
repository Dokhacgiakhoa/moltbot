---
summary: "Agent phụ (Sub-agents): Khởi tạo các lượt chạy agent cô lập và gửi kết quả ngược lại cho người yêu cầu"
read_when:
  - Bạn muốn AI thực hiện các công việc song song hoặc chạy ngầm
---
# Agent phụ (Sub-agents)

Agent phụ là các lượt chạy AI chạy ngầm được khởi tạo từ một Agent chính đang hoạt động. Chúng chạy trong một phiên làm việc riêng biệt và khi hoàn thành, chúng sẽ **thông báo** kết quả ngược lại kênh chat của người yêu cầu.

## Lợi ích chính
- **Chạy song song**: Thực hiện các nhiệm vụ nghiên cứu, tìm kiếm lâu hoặc các công cụ chậm mà không làm gián đoạn cuộc trò chuyện chính.
- **Cô lập**: Các Agent phụ hoạt động trong môi trường riêng, không làm rối loạn ngữ cảnh của phiên làm việc chính.
- **Tiết kiệm chi phí**: Bạn có thể cấu hình để các Agent phụ sử dụng các mô hình AI rẻ hơn (như các dòng Mini/Lite) cho các công việc lặp đi lặp lại.

## Cách điều khiển (Lệnh `/subagents`)
Bạn có thể quản lý các Agent phụ của phiên làm việc hiện tại bằng lệnh:
- `/subagents list`: Xem danh sách các Agent phụ đang chạy.
- `/subagents stop <id>`: Dừng một Agent phụ cụ thể.
- `/subagents log <id>`: Xem nhật ký hoạt động của Agent phụ.

## Cách Agent chính gọi Agent phụ
AI sử dụng công cụ `sessions_spawn` để tạo ra một Agent phụ mới. Các thông số bao gồm:
- `task`: Nhiệm vụ cụ thể cho Agent phụ.
- `model`: (Tùy chọn) Chọn mô hình AI cho Agent phụ này.
- `runTimeoutSeconds`: Thời gian tối đa để Agent phụ hoàn thành nhiệm vụ.

## Thông báo kết quả (Announce)
Khi hoàn thành, Agent phụ sẽ gửi một tin nhắn tóm tắt về kết quả, thời gian chạy, và lượng token đã tiêu tốn. Nếu nhiệm vụ thất bại hoặc hết thời gian, nó cũng sẽ báo cáo chi tiết lỗi để Agent chính (hoặc bạn) có thể xử lý tiếp.

---
Tài liệu liên quan: [Quản lý phiên](../concepts/session.vi.md), [Môi trường cô lập (Sandbox)](../concepts/sandboxing.vi.md).
