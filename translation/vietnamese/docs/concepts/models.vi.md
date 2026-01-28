---
summary: "Công cụ CLI cho mô hình: danh sách, cài đặt, bí danh và dự phòng"
read_when:
  - Bạn muốn thêm hoặc thay đổi mô hình bằng dòng lệnh (CLI)
  - Bạn muốn hiểu cơ chế chọn mô hình AI trong Moltbot
---

# Quản lý mô hình (Models CLI)

## Cơ chế chọn mô hình

Moltbot chọn mô hình theo thứ tự ưu tiên sau:

1) **Mô hình chính (Primary)**: Được cấu hình trong `agents.defaults.model.primary`.
2) **Mô hình dự phòng (Fallbacks)**: Danh sách các mô hình thay thế nếu mô hình chính gặp lỗi hoàn toàn.
3) **Dự phòng xác thực**: Hệ thống sẽ thử luân chuyển các tài khoản khác nhau trong cùng một nhà cung cấp trước khi chuyển sang mô hình mới.

Tài liệu liên quan: [Dự phòng lỗi mô hình](./model-failover.vi.md), [Danh sách nhà cung cấp](./model-providers.vi.md).

## Thuật sĩ thiết lập (Khuyên dùng)

Nếu bạn không muốn tự tay sửa file cấu hình JSON, hãy chạy lệnh thuật sĩ sau để bắt đầu nhanh:

```bash
moltbot onboard
```

Lệnh này sẽ hướng dẫn bạn thiết lập mô hình và thông tin đăng nhập cho các nhà cung cấp phổ biến như OpenAI, Anthropic hay Google.

## Đổi mô hình ngay trong khi chat (`/model`)

Bạn có thể thay đổi mô hình cho phiên trò chuyện hiện tại mà không cần khởi động lại Gateway:

- `/model`: Hiển thị bảng chọn mô hình nhanh bằng số thứ tự.
- `/model list`: Xem danh sách đầy đủ các mô hình khả dụng.
- `/model <số>`: Chọn nhanh mô hình theo số trong danh sách.
- `/model status`: Xem chi tiết về nhà cung cấp và trạng thái đăng nhập.

Lưu ý: Nếu một mô hình không nằm trong danh sách trắng (`agents.defaults.models`), bạn sẽ không thể chuyển sang mô hình đó.

## Các lệnh CLI chính (quản trị viên)

| Lệnh | Công dụng |
|------|-----------|
| `moltbot models list` | Xem danh sách mô hình đã cấu hình |
| `moltbot models status` | Xem trạng thái kết nối và xác thực |
| `moltbot models set <ref>` | Đổi mô hình chính của hệ thống |
| `moltbot models scan` | Quét và tìm các mô hình miễn phí trên OpenRouter |

Lệnh `moltbot models scan` rất hữu ích nếu bạn muốn tìm các mô hình chạy ổn định mà không tốn phí. Nó sẽ xếp hạng các mô hình dựa trên hỗ trợ hình ảnh, tốc độ phản hồi công cụ và dung lượng ngữ cảnh.

---
Tài liệu liên quan: [Lệnh Slash](../../tools/slash-commands.md), [Mô hình dự phòng](./model-failover.vi.md).
