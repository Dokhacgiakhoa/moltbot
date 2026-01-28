---
summary: "Các chế độ đánh thức bằng giọng nói và nhấn để nói (PTT) trong ứng dụng Mac"
read_when:
  - Bạn muốn ra lệnh cho Bot bằng giọng nói trên máy Mac của mình
---

# Đánh thức & Nhấn để nói

## Hai chế độ chính
- **Đánh thức bằng từ khóa (Wake-word)**: Bot luôn lắng nghe từ khóa (mặc định là "swabble"). Khi nhận diện được, nó sẽ hiện bảng điều khiển và tự động gửi lệnh sau khi bạn nói xong.
- **Nhấn để nói (Phím Option Phải)**: Nhấn giữ phím Option bên phải để nói trực tiếp mà không cần từ khóa. Khi thả phím, lệnh sẽ được gửi đi.

## Đặc điểm vận hành
- **Nhận diện thông minh**: Từ khóa đánh thức chỉ được kích hoạt nếu có một khoảng lặng ngắn (~0.55 giây) giữa từ khóa và câu lệnh tiếp theo để tránh nhầm lẫn.
- **Giới hạn thời gian**: Một phiên nói chuyện tối đa là 120 giây để tránh việc thu âm vô tận.
- **Âm thanh thông báo**: Bạn có thể tùy chỉnh âm thanh khi Bot bắt đầu nghe và khi gửi tin nhắn xong trong phần Cài đặt.

## Yêu cầu quyền hạn
Tính năng này yêu cầu quyền truy cập **Microphone** và **Nhận dạng giọng nói (Speech Recognition)**. Ngoài ra, để nhận diện được phím Option, bạn cần cấp quyền **Trợ năng (Accessibility)** cho ứng dụng.

---
Tài liệu liên quan: [Quyền hạn trên macOS](./permissions.vi.md), [Lớp phủ giọng nói](./voice-overlay.vi.md).
