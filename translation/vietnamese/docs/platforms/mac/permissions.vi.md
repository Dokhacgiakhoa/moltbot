---
summary: "Cơ chế duy trì quyền hạn trên macOS (TCC) và các yêu cầu về chữ ký mã nguồn"
read_when:
  - Bạn gặp lỗi không thấy thông báo hỏi quyền hạn trên máy Mac
  - Bạn đang đóng gói ứng dụng Moltbot cho macOS
---

# Quyền hạn trên macOS (TCC)

Hệ thống bảo mật của macOS (TCC) rất nhạy cảm. Nó gắn liền quyền hạn mà người dùng đã cấp với **chữ ký mã nguồn**, **định danh ứng dụng** (bundle ID) và **đường dẫn tệp tin** trên ổ cứng. Nếu một trong các yếu tố này thay đổi, macOS sẽ coi ứng dụng đó là mới và có thể yêu cầu cấp quyền lại hoặc tệ hơn là không hiện thông báo hỏi quyền.

## Các yêu cầu để giữ quyền hạn ổn định
- **Giữ nguyên đường dẫn**: Chạy ứng dụng từ một vị trí cố định (ví dụ: chạy bản đã đóng gói trong thư mục `dist/`).
- **Giữ nguyên tên định danh**: Không thay đổi Bundle ID của ứng dụng.
- **Sử dụng chữ ký thật**: Các bản build không có chữ ký hoặc dùng chữ ký tạm (ad-hoc) sẽ thường xuyên bị mất quyền hạn khi bạn biên dịch lại mã nguồn.

## Cách xử lý khi không thấy thông báo hỏi quyền
1. Thoát hoàn toàn ứng dụng.
2. Vào phần **System Settings -> Privacy & Security**, xóa mục Moltbot khỏi danh sách (nếu có).
3. Khởi động lại ứng dụng từ đường dẫn cũ và thử cấp quyền lại.
4. Nếu vẫn không được, hãy dùng lệnh `tccutil` trong Terminal để đặt lại bộ nhớ quyền hạn của hệ thống:
   ```bash
   sudo tccutil reset Accessibility bot.molt.mac
   sudo tccutil reset ScreenCapture bot.molt.mac
   ```

**Ghi chú**: Một số quyền hạn chỉ có tác dụng sau khi bạn **khởi động lại máy Mac**.

---
Tài liệu liên quan: [Ứng dụng macOS](../macos.vi.md), [Thiết lập nhà phát triển](./dev-setup.vi.md).
