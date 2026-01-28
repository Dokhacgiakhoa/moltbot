---
summary: "Hướng dẫn ClawdHub: Kho lưu trữ kỹ năng công khai và các quy trình làm việc CLI"
read_when:
  - Giới thiệu ClawdHub cho người dùng mới
  - Cài đặt, tìm kiếm hoặc xuất bản kỹ năng (skills)
---
# ClawdHub

ClawdHub là **kho lưu trữ kỹ năng công khai cho Moltbot**. Đây là một dịch vụ miễn phí: tất cả kỹ năng đều ở chế độ công khai, mở và mọi người đều có thể xem để chia sẻ hoặc dùng lại. Một "kỹ năng" (skill) thực chất chỉ là một thư mục chứa tệp `SKILL.md` (cùng các tệp văn bản hỗ trợ khác). Bạn có thể duyệt kỹ năng trên trình duyệt hoặc dùng dòng lệnh (CLI) để tìm kiếm, cài đặt, cập nhật và xuất bản chúng.

Trang web: [clawdhub.com](https://clawdhub.com)

## Dành cho ai? (Người mới bắt đầu)
Nếu bạn muốn bổ sung khả năng mới cho Moltbot, ClawdHub là cách dễ nhất để tìm và cài đặt. Bạn không cần biết sâu về kỹ thuật, bạn có thể:
- Tìm kiếm kỹ năng bằng ngôn ngữ tự nhiên.
- Cài đặt kỹ năng vào không gian làm việc của mình.
- Cập nhật kỹ năng sau này chỉ với một câu lệnh.
- Sao lưu các kỹ năng của riêng bạn bằng cách xuất bản chúng.

## Bắt đầu nhanh
1) Cài đặt công cụ dòng lệnh: `npm i -g clawdhub`.
2) Tìm thứ bạn cần: `clawdhub search "lịch cá nhân"`.
3) Cài đặt kỹ năng: `clawdhub install <tên-kỹ-năng>`.
4) Bắt đầu một phiên làm việc mới với Moltbot để nó nhận diện kỹ năng vừa cài.

## Các lệnh dòng lệnh cơ bản
- `clawdhub login`: Đăng nhập (thông qua trình duyệt).
- `clawdhub search "nội dung"`: Tìm kiếm kỹ năng.
- `clawdhub install <slug>`: Cài đặt một kỹ năng cụ thể.
- `clawdhub update --all`: Cập nhật tất cả các kỹ năng đã cài đặt.
- `clawdhub sync`: Quét các kỹ năng cục bộ và đăng tải các bản cập nhật mới lên ClawdHub.

## Lưu ý về bảo mật
Khi bạn cài đặt kỹ năng từ ClawdHub, hãy nhớ rằng đây là các kỹ năng do cộng đồng đóng góp. Trước khi sử dụng các kỹ năng yêu cầu thực thi lệnh hệ thống (như `bash` hoặc `exec`), bạn nên kiểm tra nội dung tệp `SKILL.md` để đảm bảo an toàn.

---
Tài liệu liên quan: [Kỹ năng](./skills.vi.md), [Tạo kỹ năng mới](./creating-skills.vi.md).
