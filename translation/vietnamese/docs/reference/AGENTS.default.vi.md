---
summary: "Hướng dẫn cài đặt mặc định và danh sách kỹ năng cho Agent trợ lý cá nhân Moltbot"
read_when:
  - Bạn đang bắt đầu một phiên làm việc mới với Moltbot Agent
  - Bạn muốn tìm hiểu các kỹ năng mặc định của hệ thống
---

# AGENTS.md — Trợ lý Cá nhân Moltbot (Mặc định)

## Thiết lập lần đầu (Khuyên dùng)

Moltbot sử dụng một thư mục không gian làm việc (workspace) riêng cho Agent. Mặc định là `~/clawd`.

1) Tạo thư mục làm việc:
```bash
mkdir -p ~/clawd
```

2) Sao chép các tệp mẫu vào thư mục làm việc:
```bash
cp docs/reference/templates/AGENTS.md ~/clawd/AGENTS.md
cp docs/reference/templates/SOUL.md ~/clawd/SOUL.md
cp docs/reference/templates/TOOLS.md ~/clawd/TOOLS.md
```

3) Tùy chọn: Nếu bạn muốn sử dụng danh sách kỹ năng của trợ lý cá nhân, hãy dùng tệp này làm `AGENTS.md`.

## Các nguyên tắc an toàn
- Không tự ý gửi danh sách thư mục hoặc các thông tin bí mật vào cuộc trò chuyện.
- Không thực hiện các lệnh có tính chất xóa/phá hủy trừ khi được yêu cầu rõ ràng.
- Chỉ gửi câu trả lời hoàn chỉnh lên các nền tảng nhắn tin bên ngoài (không gửi tin nhắn dạng luồng/streaming).

## Hệ thống Ghi nhớ (Memory)
- **Nhật ký hàng ngày**: Lưu tại `memory/YYYY-MM-DD.md`.
- **Trí nhớ dài hạn**: Tệp `memory.md` lưu trữ các sự thật, sở thích và quyết định quan trọng.
- Mỗi khi bắt đầu phiên làm việc mới, Agent sẽ đọc dữ liệu của ngày hôm nay, hôm qua và tệp `memory.md`.

## Các Kỹ năng Cốt lõi (Bật trong Settings → Skills)
- **Peekaboo**: Chụp ảnh màn hình macOS siêu nhanh kèm phân tích AI.
- **camsnap**: Chụp ảnh/quay clip từ camera an ninh RTSP/ONVIF.
- **imsg**: Gửi và đọc iMessage/SMS.
- **wacli**: Điều khiển WhatsApp (tìm kiếm, gửi tin).
- **gog**: Bộ công cụ Google (Gmail, Calendar, Drive).
- **spotify-player**: Điều khiển nhạc Spotify từ Terminal.
- **Gemini/OpenAI**: Tương tác trực tiếp với các mô hình AI mạnh nhất.

---
Tài liệu liên quan: [Bắt đầu nhanh](../start/getting-started.vi.md), [Quản lý Kỹ năng](../tools/skills.vi.md).
