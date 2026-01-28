---
summary: "Mẫu tệp chuẩn TOOLS.md để lưu trữ các ghi chú cục bộ về hệ thống"
read_when:
  - Bạn đang tự thiết lập một không gian làm việc mới cho Bot
---

# TOOLS.md - Ghi chú cục bộ

Các kỹ năng (Skills) định nghĩa *cách thức* công cụ hoạt động. Tệp này dành cho các thông tin *đặc thù* của bạn — những thứ riêng biệt trong hệ thống của bạn.

## Nội dung cần có ở đây

Những thứ như:
- Tên và vị trí của các Camera.
- Các máy chủ SSH và tên gợi nhớ (alias).
- Các tông giọng ưu tiên cho việc phát âm (TTS).
- Tên các loại loa hoặc phòng trong nhà.
- Tên biệt danh của các thiết bị.
- Bất kỳ thứ gì đặc trưng cho môi trường của bạn.

## Ví dụ

```markdown
### Cameras
- living-room → Khu vực chính, góc rộng 180°
- front-door → Cửa trước, tự động báo động khi có chuyển động

### SSH
- home-server → IP 192.168.1.100, user: admin

### TTS (Phát âm)
- Giọng ưu tiên: "Nova" (ấm áp, hơi hướm giọng Anh)
- Loa mặc định: Apple HomePod ở phòng bếp
```

## Tại sao cần tách riêng?

Các kỹ năng là phần dùng chung. Nhưng thiết lập hệ thống là của riêng bạn. Việc tách riêng giúp bạn cập nhật các kỹ năng mà không bị mất các ghi chú cá nhân, và có thể chia sẻ kỹ năng với người khác mà không bị lộ thông tin hạ tầng mạng của mình.

---

Hãy thêm bất kỳ điều gì giúp bạn hoàn thành công việc. Đây là tệp "bí kíp" của riêng bạn.
