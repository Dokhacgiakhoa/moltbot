---
summary: "Tất cả các tùy chọn cấu hình cho ~/.clawdbot/moltbot.json kèm ví dụ minh họa"
read_when:
  - Bạn cần thêm hoặc sửa đổi các trường cấu hình của hệ thống
---

# Cấu hình (Configuration) 🔧

Moltbot đọc cấu hình từ tệp tin tùy chọn `~/.clawdbot/moltbot.json` sử dụng định dạng **JSON5** (cho phép ghi chú và dấu phẩy thừa ở cuối).

Nếu tệp này không tồn tại, Moltbot sẽ sử dụng các giá trị mặc định an toàn. Bạn thường chỉ cần tạo file cấu hình khi muốn:
- Giới hạn những ai có thể nhắn tin cho Bot (`allowFrom`).
- Kiểm soát các nhóm chat và quy tắc nhắc tên (@mention).
- Tùy chỉnh tiền tố tin nhắn trả về.
- Thay đổi không gian làm việc của Agent.
- Thiết lập tính cách riêng cho Agent.

> **Mới làm quen?** Hãy xem [Các ví dụ cấu hình](./configuration-examples.vi.md) để bắt đầu nhanh hơn!

## Kiểm chứng cấu hình nghiêm ngặt

Moltbot chỉ chấp nhận các cấu hình khớp hoàn toàn với cấu trúc (schema) quy định. Các trường lạ, sai kiểu dữ liệu hoặc giá trị không hợp lệ sẽ khiến Gateway **từ chối khởi động** để đảm bảo an toàn.

Khi việc kiểm chứng thất bại:
- Gateway sẽ không chạy.
- Bạn chỉ có thể dùng các lệnh chẩn đoán (như `moltbot doctor`, `moltbot logs`).
- Hãy chạy lệnh `moltbot doctor` để xem chính xác lỗi nằm ở đâu.

## Nhúng tệp cấu hình (`$include`)

Bạn có thể chia nhỏ tệp cấu hình của mình thành nhiều tệp khác nhau bằng chỉ dẫn `$include`. Điều này rất hữu ích để:
- Tổ chức các tệp cấu hình lớn (ví dụ: mỗi khách hàng một tệp riêng).
- Giữ các thông tin nhạy cảm tách biệt.

### Cách dùng cơ bản:
```json5
{
  "gateway": { "port": 18789 },
  // Nhúng một tệp duy nhất
  "agents": { "$include": "./agents.json5" },
  // Nhúng nhiều tệp (sẽ được gộp theo thứ tự)
  "broadcast": { 
    "$include": ["./client-a.json5", "./client-b.json5"]
  }
}
```

## Thay thế biến môi trường

Bạn có thể tham chiếu trực tiếp các biến môi trường trong bất kỳ giá trị chuỗi nào của cấu hình bằng cú pháp `${TEN_BIEN}`.

```json5
{
  "models": {
    "providers": {
      "anthropic": {
        "apiKey": "${ANTHROPIC_API_KEY}"
      }
    }
  }
}
```

## Các tùy chọn phổ biến

### Nhật ký (Logging)
Bạn có thể điều chỉnh mức độ ghi nhật ký và vị trí tệp lưu trữ:
- `logging.level`: Mức độ chi tiết (`info`, `debug`, `warn`).
- `logging.file`: Đường dẫn tệp nhật ký.
- `logging.redactSensitive`: Tự động ẩn các thông tin nhạy cảm (như Token) trong nhật ký.

### Quy tắc nhắc tên trong nhóm chat
Mặc định, trong các nhóm chat, Bot sẽ chỉ trả lời khi được nhắc tên (@mention). Bạn có thể tùy chỉnh các mẫu từ ngữ để kích hoạt Bot:
```json5
{
  "agents": {
    "list": [
      { "id": "main", "groupChat": { "mentionPatterns": ["@moltbot", "ơi AI"] } }
    ]
  }
}
```

### Chính sách tin nhắn cá nhân (DM Policy)
- `pairing` (Mặc định): Người lạ nhắn tin sẽ nhận được mã ghép nối, bạn phải phê duyệt mới có thể tiếp tục.
- `allowlist`: Chỉ những người trong danh sách `allowFrom` mới được phép nhắn tin.
- `open`: Cho phép tất cả mọi người.

---
*Lưu ý: Đây là phần đầu của tài liệu cấu hình. Để xem chi tiết từng trường dữ liệu kỹ thuật, vui lòng tham khảo file cấu hình gốc bằng tiếng Anh hoặc sử dụng công cụ hỗ trợ trong Control UI.*
