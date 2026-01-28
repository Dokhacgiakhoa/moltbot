---
summary: "Chạy nhiều Gateway Moltbot trên cùng một máy (Cô lập, cổng và hồ sơ)"
read_when:
  - Bạn muốn chạy hai hoặc nhiều bản Moltbot đồng thời trên một máy tính
---

# Chạy nhiều Gateway trên cùng một máy

Hầu hết các trường hợp chỉ cần một Gateway duy nhất vì nó có thể xử lý nhiều tài khoản nhắn tin và nhiều Agent cùng lúc. Bạn chỉ nên chạy nhiều Gateway nếu muốn cô lập dữ liệu tuyệt đối hoặc cần thiết lập một **Bot cứu hộ (Rescue Bot)**.

## Danh mục kiểm tra sự cô lập (Bắt buộc)
Để tránh xung đột, mỗi Gateway phải có:
- `CLAWDBOT_CONFIG_PATH`: Tệp cấu hình riêng.
- `CLAWDBOT_STATE_DIR`: Thư mục lưu phiên chat và thông tin đăng nhập riêng.
- `agents.defaults.workspace`: Không gian làm việc của Agent riêng.
- `gateway.port`: Cổng giao tiếp duy nhất (ví dụ: 18789 và 19001).
- Các cổng phụ (như trình duyệt/canvas) cũng phải khác nhau.

## Khuyên dùng: Sử dụng Hồ sơ (`--profile`)
Hồ sơ (Profile) sẽ tự động phạm vi hóa các thư mục dữ liệu và cấu hình, đồng thời đặt tên khác nhau cho các dịch vụ hệ thống.

```bash
# Gateway chính
moltbot --profile main gateway --port 18789

# Gateway cứu hộ
moltbot --profile rescue gateway --port 19001
```

## Hướng dẫn thiết lập Bot cứu hộ (Rescue-Bot)
Bot cứu hộ chạy song song với Bot chính. Nếu Bot chính gặp lỗi cấu hình hoặc bị treo, bạn vẫn có thể liên lạc với Bot cứu hộ để yêu cầu nó sửa lỗi hoặc khởi động lại Bot chính.

**Lưu ý về cổng**: Nên chọn các cổng giao tiếp cách xa nhau (ít nhất 20 đơn vị) để tránh việc các cổng phụ (trình duyệt, canvas) bị trùng lặp.

---
Tài liệu liên quan: [Cấu hình hệ thống](./configuration.vi.md), [Khám phá mạng nội bộ](./bonjour.vi.md).
