---
summary: "Dịch vụ điều khiển trình duyệt tích hợp và các lệnh thao tác của agent"
read_when:
  - Bạn muốn cho phép agent tự động hóa các thao tác trên trình duyệt
  - Cần gỡ lỗi hoặc cấu hình trình duyệt tích hợp
---
# Trình duyệt (Quản lý bởi clawd)

Moltbot có thể chạy một **hồ sơ trình duyệt riêng biệt** (Chrome/Brave/Edge/Chromium) để agent điều khiển. Trình duyệt này hoàn toàn tách biệt với trình duyệt cá nhân của bạn và được quản lý thông qua một dịch vụ nội bộ nhỏ trong Gateway.

## Đặc điểm nổi bật
- **Tách biệt hoàn toàn**: Agent sử dụng hồ sơ `clawd` riêng, không chạm vào lịch sử hay mật khẩu cá nhân của bạn.
- **Khả năng mạnh mẽ**: Agent có thể mở tab, đọc nội dung trang web, nhấn chuột, nhập liệu và chụp ảnh màn hình.
- **Điều khiển chính xác**: Agent sử dụng các tham chiếu (refs) thay vì các bộ chọn CSS mỏng manh để thao tác chính xác các thành phần trên web.

## Bắt đầu nhanh
Sử dụng các lệnh sau từ dòng lệnh để điều khiển trình duyệt của Moltbot:
```bash
# Xem trạng thái trình duyệt
moltbot browser --browser-profile clawd status
# Khởi động trình duyệt
moltbot browser --browser-profile clawd start
# Mở một trang web cụ thể
moltbot browser --browser-profile clawd open https://google.com
```

## Hai loại hồ sơ chính
- `clawd`: Trình duyệt được Moltbot quản lý và tách biệt hoàn toàn (không cần cài thêm tiện ích).
- `chrome`: Điều khiển **trình duyệt cá nhân** bạn đang dùng thông qua một tiện ích mở rộng (Yêu cầu cài đặt thêm tiện ích Moltbot).

## Cách agent "nhìn" trang web
Agent không nhìn trang web như một tấm ảnh bình thường. Nó chụp một **"Snapshot"**.
- **AI Snapshot**: Tạo ra một sơ đồ văn bản của trang web với các mã số (`1`, `2`, `3`...).
- **Role Snapshot**: Tạo ra một danh sách các thành phần tương tác (nút bấm, ô nhập liệu) với các mã như `e12`, `e13`.
Sau đó, agent sẽ ra lệnh: "Nhấn vào nút có mã `e12`" hoặc "Nhập văn bản vào ô `e13`".

## Lưu ý về bảo mật
- Agent có khả năng thực thi các đoạn mã JavaScript trên trang web. Bạn có thể tắt tính năng này nếu lo ngại về bảo mật.
- Hồ sơ `clawd` có thể lưu lại các phiên đăng nhập; hãy coi trọng bảo mật cho hồ sơ này như trình duyệt chính của bạn.

---
Tài liệu liên quan: [Tiện ích Chrome](./chrome-extension.vi.md), [Đăng nhập trình duyệt](./browser-login.vi.md), [Khắc phục lỗi Linux](./browser-linux-troubleshooting.vi.md).
