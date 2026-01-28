---
summary: "Tài liệu tham khảo lệnh `moltbot onboard` (Thuật sĩ thiết lập tương tác)"
read_when:
  - Bạn muốn được hướng dẫn từng bước để thiết lập gateway, không gian làm việc, xác thực, các kênh và kỹ năng
---

# `moltbot onboard`

Đây là trình thuật sĩ thiết lập tương tác (hỗ trợ cả thiết lập Gateway tại chỗ hoặc từ xa).

Tài liệu liên quan:
- Hướng dẫn thuật sĩ: [Quy trình Onboarding](../../start/onboarding.vi.md)

## Ví dụ sử dụng

```bash
moltbot onboard
moltbot onboard --flow quickstart
moltbot onboard --flow advanced
moltbot onboard --mode remote --remote-url ws://di-chi-gateway:18789
```

## Các lưu ý về luồng thiết lập (Flow):
- `quickstart`: Tối giản các câu hỏi, tự động tạo mã bảo mật (token) cho gateway.
- `advanced`: Đầy đủ các câu hỏi cấu hình về cổng (port), địa chỉ liên kết (bind), và phương thức xác thực.
- Cách nhanh nhất để bắt đầu: `moltbot dashboard` (Mở giao diện điều khiển, không cần thiết lập kênh ngay).
