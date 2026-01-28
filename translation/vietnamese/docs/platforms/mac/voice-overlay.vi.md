---
summary: "Vòng đời của lớp phủ giọng nói (Voice overlay) khi sử dụng từ khóa đánh thức và nhấn để nói"
read_when:
  - Bạn đang điều chỉnh hành vi hiển thị của bảng điều khiển giọng nói trên máy Mac
---

# Lớp phủ Giọng nói (macOS)

Mô tả về cách thức hoạt động của bảng điều khiển giọng nói khi người dùng sử dụng từ khóa đánh thức (Wake-word) hoặc phím nóng (Push-to-talk).

## Cơ chế hoạt động
- **Kế thừa nội dung**: Nếu bảng điều khiển đang hiện ra do từ khóa đánh thức và bạn nhấn giữ phím nóng, hệ thống sẽ giữ nguyên đoạn văn bản đang có và tiếp tục ghi âm thêm thay vì xóa đi làm lại từ đầu.
- **Gửi tin nhắn**:
  - Đối với từ khóa đánh thức: Bot tự động gửi sau một khoảng thời gian im lặng.
  - Đối với phím nóng: Bot gửi ngay lập tức khi bạn thả phím.
- **An toàn dữ liệu**: Mỗi phiên ghi âm đều có một mã định danh (token) riêng để đảm bảo các kết quả ghi âm cũ không ghi đè lên phiên làm việc mới.

## Gỡ lỗi
Nếu lớp phủ bị "kẹt" trên màn hình, bạn có thể kiểm tra nhật ký hệ thống bằng lệnh:
```bash
sudo log stream --predicate 'subsystem == "bot.molt" AND category CONTAINS "voicewake"' --level info
```

---
Tài liệu liên quan: [Đánh thức bằng giọng nói](./voicewake.vi.md), [Hệ thống nhật ký](./logging.vi.md).
