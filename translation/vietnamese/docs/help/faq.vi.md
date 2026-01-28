---
summary: "Các câu hỏi thường gặp về việc thiết lập, cấu hình và sử dụng Moltbot"
---
# Câu hỏi thường gặp (FAQ)

Dưới đây là các câu trả lời nhanh cũng như các hướng dẫn xử lý sự cố chuyên sâu cho các trường hợp thực tế (phát triển tại máy cục bộ, VPS, đa Agent, khóa API, dự phòng mô hình). Để xem chẩn đoán lỗi khi đang chạy, hãy xem [Xử lý sự cố](./troubleshooting.vi.md). Để xem tài liệu cấu hình đầy đủ, hãy xem [Cấu hình](../../gateway/configuration.vi.md).

## Mục lục

- [Bắt đầu nhanh và thiết lập lần đầu](#bat-dau-nhanh-va-thiet-lap-lan-dau)
- [Moltbot là gì?](#moltbot-la-gi)
- [Kỹ năng và Tự động hóa](#ky-nang-va-tu-dong-hoa)
- [Hộp cát (Sandbox) và Ghi nhớ](#hop-cat-sandbox-va-ghi-nho)
- [Dữ liệu lưu ở đâu?](#du-lieu-luu-o-dau)
- [Các mô hình AI](#cac-mo-hinh-ai)

---

## Bắt đầu nhanh và thiết lập lần đầu

### Tôi bị kẹt, cách nào nhanh nhất để thoát kẹt?
Hãy sử dụng một công cụ AI cục bộ có khả năng "nhìn" thấy máy tính của bạn (như **Claude Code** hoặc **OpenAI Codex**). Điều này hiệu quả hơn nhiều so với việc hỏi trên Discord, vì hầu hết các trường hợp bị kẹt đều liên quan đến cấu hình hoặc môi trường máy tính của bạn mà người hỗ trợ từ xa không thể kiểm tra được.

Bạn nên cài đặt Moltbot bằng phương pháp **git install** để AI có thể đọc mã nguồn và tài liệu ngay trong thư mục đó:
```bash
curl -fsSL https://molt.bot/install.sh | bash -s -- --install-method git
```

### Cách khuyên dùng để cài đặt Moltbot là gì?
Chúng tôi khuyên bạn nên chạy từ mã nguồn và sử dụng trình hướng dẫn thiết lập (onboarding wizard):
```bash
curl -fsSL https://molt.bot/install.sh | bash
moltbot onboard --install-daemon
```

### Tôi có cần đăng ký trả phí Claude hay OpenAI để chạy không?
Không bắt buộc. Bạn có thể sử dụng Moltbot bằng **API key** (trả phí theo mức sử dụng) hoặc sử dụng các **mô hình chạy cục bộ** để dữ liệu hoàn toàn không rời khỏi thiết bị của bạn.

### Làm thế nào để mở bảng điều khiển (Dashboard) sau khi thiết lập?
Trình hướng dẫn sẽ tự động mở trình duyệt với đường dẫn chứa mã Token ngay sau khi hoàn tất. Nếu nó không tự mở, bạn có thể chạy lệnh:
`moltbot dashboard`
Lệnh này sẽ sao chép đường dẫn kèm mã truy cập an toàn vào bộ nhớ tạm của bạn.

### Moltbot có chạy được trên Raspberry Pi không?
Có. Gateway rất nhẹ và có thể chạy tốt trên **Raspberry Pi 4** với RAM từ 1GB trở lên.

### Tôi có thể chuyển dữ liệu sang máy tính mới mà không cần thiết lập lại không?
Có. Bạn chỉ cần sao chép thư mục trạng thái (mặc định là `~/.clawdbot`) và không gian làm việc của Bot (mặc định là `~/clawd`) sang máy mới, sau đó chạy lệnh `moltbot doctor` để hệ thống tự đồng bộ lại.

---

> *Lưu ý: Đây là bản dịch tóm tắt của tệp FAQ. Để xem đầy đủ các câu hỏi chuyên sâu, vui lòng tham khảo tệp gốc bằng tiếng Anh.*
