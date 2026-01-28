---
summary: "Cấu trúc file cấu hình kỹ năng và các ví dụ minh họa"
read_when:
  - Bạn muốn thay đổi cách nạp hoặc cài đặt các kỹ năng (skills)
---
# Cấu hình kỹ năng (Skills Config)

Tất cả các cài đặt liên quan đến kỹ năng nằm trong mục `skills` của tệp `~/.clawdbot/moltbot.json`.

## Các trường dữ liệu chính

- `allowBundled`: Danh sách (tùy chọn) các kỹ năng **đi kèm sẵn** được phép hoạt động. Nếu thiết lập, chỉ các kỹ năng trong danh sách này mới được nạp.
- `load.extraDirs`: Các thư mục bổ sung để AI quét tìm kỹ năng (có độ ưu tiên thấp nhất).
- `load.watch`: Tự động theo dõi các thay đổi trong thư mục kỹ năng và cập nhật ngay lập tức (mặc định là `true`).
- `install.preferBrew`: Ưu tiên sử dụng trình cài đặt `brew` nếu có sẵn (mặc định là `true`).
- `install.nodeManager`: Trình quản lý gói Node ưu tiên (`npm`, `pnpm`, `yarn` hoặc `bun`).
- `entries.<tên_kỹ_năng>`: Các thiết lập ghi đè riêng cho từng kỹ năng cụ thể.

## Thiết lập cho từng kỹ năng
Bên trong mục `entries`, bạn có thể cấu hình:
- `enabled`: Đặt thành `false` để vô hiệu hóa một kỹ năng kể cả khi nó đã được cài đặt.
- `env`: Các biến môi trường riêng được nạp khi AI chạy kỹ năng này.
- `apiKey`: Cách nhanh chóng để cung cấp mã API cho các kỹ năng yêu cầu.

## Lưu ý về môi trường cô lập (Sandbox)
Khi một phiên làm việc đang chạy trong **Sandbox** (Docker):
- Các tiến trình kỹ năng sẽ chạy bên trong Docker.
- Sandbox sẽ **không** tự động nhận các biến môi trường từ máy chủ thật.
- Bạn cần khai báo các biến môi trường này trong cấu hình `agents.defaults.sandbox.docker.env` để AI có thể sử dụng chúng bên trong môi trường cô lập.

---
Tài liệu liên quan: [Tạo kỹ năng mới](./creating-skills.vi.md), [ClawdHub](./clawdhub.vi.md).
