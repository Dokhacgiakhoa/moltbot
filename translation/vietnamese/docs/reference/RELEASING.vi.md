---
summary: "Danh sách kiểm tra quy trình phát hành từng bước cho gói npm và ứng dụng macOS"
read_when:
  - Bạn chuẩn bị phát hành một phiên bản npm mới
  - Bạn phát hành bản cập nhật cho ứng dụng macOS
---

# Danh sách kiểm tra Phát hành (npm + macOS)

Sử dụng `pnpm` (Node 22+) từ thư mục gốc của kho mã nguồn. Đảm bảo mọi thay đổi đã được commit sạch sẽ trước khi gắn thẻ (tag) hoặc phát hành.

## Các bước thực hiện

1) **Phiên bản & Dữ liệu mô tả**
- Cập nhật số phiên bản trong `package.json` (ví dụ: `2026.1.27-beta.1`).
- Chạy `pnpm plugins:sync` để đồng bộ phiên bản của các tiện ích mở rộng.
- Kiểm tra lại các thông tin mô tả gói (tên, giấy phép, các tệp nhị phân).

2) **Xây dựng bản dựng (Build)**
- Chạy `pnpm run build` để tạo lại thư mục `dist/`.
- Xác nhận các thư mục quan trọng như `dist/node-host/` đã được bao gồm.
- Kiểm tra sự tồn tại của tệp `dist/build-info.json`.

3) **Nhật ký thay đổi (Changelog)**
- Cập nhật tệp `CHANGELOG.md` với các điểm nổi bật dành cho người dùng.
- Đảm bảo các ví dụ trong README vẫn đúng với hành vi mới của CLI.

4) **Kiểm chứng (Validation)**
- Chạy `pnpm lint` và `pnpm test`.
- Chạy bài kiểm tra cài đặt thử nghiệm: `pnpm test:install:smoke`.

5) **Ứng dụng macOS (Sparkle)**
- Biên dịch và ký tên ứng dụng Mac, sau đó đóng gói dạng ZIP.
- Tạo tệp tin `appcast.xml` cho hệ thống tự động cập nhật Sparkle.
- Thực hiện các bước ký tên và xác thực (notarization) theo [Hướng dẫn phát hành Mac](../platforms/mac/release.vi.md).

6) **Phát hành lên npm**
- `npm login` và kiểm tra xác thực 2 lớp (2FA).
- Chạy `npm publish --access public`.

7) **Phát hành lên GitHub**
- Gắn thẻ phiên bản: `git tag vX.Y.Z && git push origin vX.Y.Z`.
- Tạo **Release** trên GitHub với tiêu đề và nội dung nhật ký thay đổi đầy đủ.
- Đính kèm các tệp ZIP của ứng dụng Mac và gói npm vào Release.

---
Tài liệu liên quan: [Phát hành Mac](../platforms/mac/release.vi.md), [Thiết lập nhà phát triển](../platforms/mac/dev-setup.vi.md).
