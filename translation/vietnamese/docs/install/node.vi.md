---
title: "Kiểm tra Node.js + npm (Đường dẫn PATH)"
summary: "Hướng dẫn kiểm tra phiên bản Node.js/npm và xử lý lỗi lệnh moltbot không tìm thấy"
read_when:
  - Bạn đã cài đặt Moltbot nhưng khi gõ lệnh hệ thống báo "command not found"
  - Bạn đang thiết lập Node.js/npm trên máy tính mới
---

# Kiểm tra Node.js + npm (Đường dẫn PATH)

Moltbot yêu cầu phiên bản **Node 22 trở lên**.

Nếu bạn đã chạy lệnh cài đặt thành công nhưng sau đó gõ `moltbot` mà hệ thống báo "command not found", thì nguyên nhân hầu như luôn là do **đường dẫn PATH**: Thư mục chứa các tệp thực thi của npm chưa được khai báo với hệ điều hành.

## Kiểm tra nhanh
Hãy chạy các lệnh sau:
```bash
node -v    # Kiểm tra phiên bản Node
npm -v     # Kiểm tra phiên bản npm
npm prefix -g   # Xem thư mục cài đặt gốc của npm
```
Nếu thư mục kết quả của lệnh `npm prefix -g` không nằm trong danh sách của lệnh `echo $PATH`, máy tính của bạn sẽ không biết tìm lệnh `moltbot` ở đâu.

## Cách sửa: Thêm npm vào đường dẫn PATH

### Trên macOS / Linux
1. Tìm đường dẫn thực tế bằng lệnh `npm prefix -g`.
2. Thêm dòng sau vào tệp cấu hình trình khởi chạy của bạn (thường là `~/.zshrc` hoặc `~/.bashrc`):
```bash
export PATH="$(npm prefix -g)/bin:$PATH"
```
3. Mở một cửa sổ Terminal mới để thay đổi có hiệu lực.

### Trên Windows
Hãy thêm đường dẫn kết quả từ lệnh `npm prefix -g` vào biến môi trường **PATH** trong phần cài đặt "System Environment Variables" của Windows.

## Xử lý lỗi quyền hạn (Linux)
Nếu bạn gặp lỗi `EACCES` khi cài đặt (không có quyền ghi vào thư mục hệ thống), hãy chuyển thư mục cài đặt npm về thư mục cá nhân của bạn:
```bash
mkdir -p "$HOME/.npm-global"
npm config set prefix "$HOME/.npm-global"
export PATH="$HOME/.npm-global/bin:$PATH"
```

---
Tài liệu liên quan: [Chi tiết trình cài đặt](./installer.vi.md), [Xử lý lỗi](../gateway/troubleshooting.vi.md).
