---
summary: "Cách thức hoạt động của các kịch bản cài đặt (install.sh + install-cli.sh), các tham số và tự động hóa"
read_when:
  - Bạn muốn hiểu rõ cách lệnh `molt.bot/install.sh` hoạt động
  - Bạn muốn tự động hóa việc cài đặt (cho CI hoặc các máy chủ không có giao diện)
  - Bạn muốn cài đặt trực tiếp từ mã nguồn GitHub
---

# Chi tiết trình cài đặt

Moltbot cung cấp hai kịch bản cài đặt chính (thông qua địa chỉ `molt.bot`):

- **`https://molt.bot/install.sh`**: Trình cài đặt khuyên dùng (mặc định cài đặt qua npm toàn cục; cũng có thể cài từ mã nguồn GitHub).
- **`https://molt.bot/install-cli.sh`**: Dành cho người dùng không có quyền root (cài đặt vào một thư mục riêng kèm theo bản Node riêng).
- **`https://molt.bot/install.ps1`**: Trình cài đặt dành cho Windows PowerShell.

Để xem các tham số hỗ trợ, bạn có thể chạy:
```bash
curl -fsSL https://molt.bot/install.sh | bash -s -- --help
```

## install.sh (Khuyên dùng)
Kịch bản này thực hiện các bước:
1. Nhận diện hệ điều hành (macOS / Linux / WSL).
2. Đảm bảo máy có Node.js phiên bản **22 trở lên**.
3. Lựa chọn phương thức cài đặt:
   - `npm` (mặc định): Chạy lệnh `npm install -g moltbot@latest`.
   - `git`: Tải mã nguồn về, đóng gói và cài đặt một kịch bản bao bọc (wrapper).
4. Trên Linux: Tự động chuyển thư mục cài đặt npm sang `~/.npm-global` để tránh lỗi quyền hạn (EACCES) nếu cần.
5. Chạy lệnh `moltbot doctor` để kiểm tra và di chuyển cấu hình cũ sang mới.

## install-cli.sh (Dành cho máy không có quyền Root)
Kịch bản này cài đặt `moltbot` vào thư mục mặc định là `~/.clawdbot` và tự cài một bản Node riêng bên trong đó. Cách này hữu ích khi bạn không muốn làm ảnh hưởng đến phiên bản Node chung của hệ thống.

## install.ps1 (Dành cho Windows)
Thực hiện tương tự các bước trên Windows, đảm bảo có Node 22+ và lựa chọn giữa cài từ npm hoặc git.

**Lưu ý cho người dùng Windows**: 
- Nếu gặp lỗi "moltbot is not recognized", hãy kiểm tra xem thư mục bin của npm đã nằm trong biến môi trường PATH chưa (thường là `%AppData%\npm`).

---
Tài liệu liên quan: [Cài đặt Node.js](./node.vi.md), [Xử lý lỗi](../gateway/troubleshooting.vi.md).
