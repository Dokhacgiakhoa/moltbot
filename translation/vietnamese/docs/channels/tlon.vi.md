---
summary: "Trạng thái hỗ trợ Tlon/Urbit, các khả năng và hướng dẫn cấu hình"
read_when:
  - Bạn đang sử dụng Tlon (Urbit) và muốn tích hợp trợ lý AI
---
# Tlon (Plugin)

Tlon là một ứng dụng nhắn tin phi tập trung được xây dựng trên nền tảng **Urbit**. Moltbot kết nối với tàu (ship) Urbit của bạn và có thể phản hồi các tin nhắn trực tiếp (DM) cũng như tin nhắn trong nhóm.

## Cài đặt Plugin
Tlon được cung cấp dưới dạng plugin:
```bash
moltbot plugins install @moltbot/tlon
```

## Các bước thiết lập
1. **Thông tin tàu**: Bạn cần địa chỉ URL của tàu và mã đăng nhập (login code).
2. **Cấu hình**:
   ```json5
   {
     channels: {
       tlon: {
         enabled: true,
         ship: "~name-of-your-ship",
         url: "https://ship-host-cua-ban",
         code: "ma-dang-nhap-bon-phan"
       }
     }
   }
   ```

## Hoạt động trong nhóm
- **Nhắc tên**: Mặc định bot chỉ phản hồi trong nhóm khi được nhắc tên (ví dụ: `~ship-cua-bot`).
- **Tự động khám phá**: Moltbot sẽ tự động tìm kiếm các kênh mà nó tham gia, hoặc bạn có thể chỉ định danh sách kênh thủ công trong `groupChannels`.
- **Phản hồi theo luồng**: Nếu tin nhắn gốc nằm trong một luồng (thread), Moltbot sẽ trả lời ngay trong luồng đó.

## Kiểm soát quyền truy cập
Bạn có thể giới hạn những tàu (ship) nào được phép tương tác với bot thông qua `dmAllowlist` (cho tin nhắn cá nhân) và `authorization` (cho các quy tắc trong nhóm).

## Các giới hạn hiện tại
- Hiện tại chưa hỗ trợ gửi các tệp tin media trực tiếp (sẽ được gửi dưới dạng URL đính kèm).
- Chưa hỗ trợ các tính năng như Biểu tượng cảm xúc (Reactions) hoặc Bình chọn (Polls).

---
Tài liệu liên quan: [Khái niệm phiên làm việc](../../concepts/session.vi.md), [Plugin](../../plugin.vi.md).
