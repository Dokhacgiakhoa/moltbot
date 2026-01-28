---
summary: "Hỗ trợ Signal qua signal-cli (JSON-RPC + SSE), thiết lập và mô hình số điện thoại"
read_when:
  - Thiết lập hỗ trợ Signal cho bot
---
# Signal (signal-cli)

Trạng thái: Tích hợp qua công cụ CLI bên ngoài. Gateway giao tiếp với `signal-cli` thông qua giao thức HTTP JSON-RPC kết hợp với SSE (Server-Sent Events).

## Thiết lập nhanh (cho người mới)
1) Chuẩn bị một **số điện thoại Signal riêng biệt** cho bot (khuyên dùng để tránh vòng lặp tin nhắn).
2) Cài đặt `signal-cli` (yêu cầu máy có sẵn Java).
3) Liên kết thiết bị bot bằng lệnh: `signal-cli link -n "Moltbot"`, sau đó quét mã QR bằng ứng dụng Signal trên điện thoại.
4) Cấu hình số điện thoại và đường dẫn CLI trong Moltbot.
5) Chạy Gateway. Tương tự các kênh khác, lần đầu sử dụng bot sẽ yêu cầu ghép nối (pairing).

## Mô hình số điện thoại (Lưu ý quan trọng)
- Bot hoạt động như một thiết bị Signal thực thụ.
- Nếu bạn dùng chính số điện thoại cá nhân làm bot, nó sẽ không phản hồi lại chính tin nhắn của bạn để tránh lỗi vòng lặp vô hạn.
- Tốt nhất hãy dùng một số điện thoại phụ để bạn có thể nhắn tin cho bot và nhận phản hồi.

## Tính năng hỗ trợ
- **Chỉ báo đang nhập**: Moltbot sẽ gửi tín hiệu "đang nhập" trong khi AI đang xử lý câu trả lời.
- **Biên nhận đã đọc**: Bot có thể gửi tín hiệu "đã xem" cho các tin nhắn trực tiếp.
- **Cảm xúc (Reactions)**: Hỗ trợ thả thính, thả tim cho tin nhắn thông qua công cụ tin nhắn của agent.
- **Tệp đính kèm**: Hỗ trợ nhận và gửi hình ảnh, tài liệu.

## Cấu hình mẫu
```json5
{
  channels: {
    signal: {
      enabled: true,
      account: "+8490xxxxxxx", // Số điện thoại của bot
      cliPath: "signal-cli",
      dmPolicy: "pairing"
    }
  }
}
```

## Chế độ chạy ngầm (Daemon)
`signal-cli` khởi động khá chậm do chạy trên nền Java. Moltbot mặc định sẽ tự khởi động nó, nhưng bạn cũng có thể chạy `signal-cli` ở chế độ daemon riêng biệt và chỉ định URL HTTP cho Moltbot để tăng tốc độ kết nối.

---
Tài liệu liên quan: [Ghép nối thiết bị](../../start/pairing.vi.md), [Cấu hình Gateway](../../gateway/configuration.vi.md).
