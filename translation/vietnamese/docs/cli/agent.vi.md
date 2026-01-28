---
summary: "Tài liệu tham khảo lệnh `moltbot agent` (Chạy một lượt xử lý của Agent qua Gateway)"
read_when:
  - Bạn muốn chạy một lệnh AI từ các script hoặc lệnh terminal (có tùy chọn gửi phản hồi)
---

# `moltbot agent`

Chạy một lượt xử lý (turn) của Agent thông qua Gateway. Sử dụng cờ `--local` nếu muốn chạy trực tiếp không qua máy chủ.

Sử dụng `--agent <id>` để chỉ định chính xác Agent nào (nếu bạn có nhiều trợ lý).

## Ví dụ sử dụng

```bash
# Gửi một thông báo cập nhật trạng thái
moltbot agent --to +8490xxxxxxx --message "Cập nhật tiến độ dự án" --deliver

# Yêu cầu Agent "ops" tóm tắt nhật ký
moltbot agent --agent ops --message "Hãy tóm tắt các dòng log gần nhất"

# Phản hồi vào một kênh cụ thể (ví dụ Slack)
moltbot agent --agent ops --message "Tạo báo cáo tuần" --deliver --reply-channel slack --reply-to "#reports"
```

Tài liệu liên quan:
- Công cụ gửi tin nhắn: [Agent send](../../tools/agent-send.vi.md).
