---
summary: "Kế hoạch tái cấu trúc: Điều hướng thực thi lệnh, phê duyệt nút mạng và dịch vụ chạy ngầm"
---

# Tái cấu trúc Hệ thống thực thi lệnh (Exec Host)

## Mục tiêu
- Bổ sung khả năng điều hướng thực thi lệnh giữa các môi trường: **Hộp cát (Sandbox)**, **Máy chủ Gateway**, và **Nút mạng (Node)**.
- Đảm bảo mặc định luôn **An toàn**: Không cho phép thực thi lệnh xuyên thiết bị trừ khi người dùng cho phép rõ ràng.
- Tách biệt việc thực thi lệnh thành một dịch vụ chạy ngầm (headless) và giao diện phê duyệt (macOS app) kết nối với nhau qua giao thức nội bộ.
- Hỗ trợ các chế độ "Hỏi trước khi chạy" linh hoạt.

## Các khái niệm chính

### 1. Môi trường thực thi (Host)
- `sandbox`: Chạy trong Docker (mặc định và an toàn nhất).
- `gateway`: Chạy trực tiếp trên máy tính cài đặt Gateway.
- `node`: Chạy trên một máy tính hoặc thiết bị khác đang kết nối vào mạng.

### 2. Các chế độ bảo mật (Security mode)
- `deny`: Luôn luôn chặn, không cho chạy.
- `allowlist`: Chỉ cho chạy các lệnh nằm trong danh sách đã cho phép.
- `full`: Cho phép chạy mọi lệnh (tương đương với quyền quản trị).

### 3. Chế độ hỏi (Ask mode)
- `off`: Không bao giờ hỏi.
- `on-miss`: Chỉ hỏi khi lệnh không nằm trong danh sách cho phép.
- `always`: Luôn luôn hiện bảng hỏi mỗi khi muốn chạy lệnh.

## Quy trình phê duyệt
Khi một lệnh được gửi đi (ví dụ từ AI):
1. Hệ thống xác định xem lệnh đó sẽ được chạy ở đâu.
2. Kiểm tra danh sách các lệnh đã được phê duyệt trước đó trong tệp `exec-approvals.json`.
3. Nếu cần phải hỏi người dùng, một thông báo sẽ được gửi tới ứng dụng Moltbot trên máy Mac của bạn.
4. Nếu bạn bấm đồng ý, lệnh sẽ được thực thi và kết quả trả về cho Bot.

## Lộ trình thực hiện
- **Giai đoạn 1**: Cập nhật cấu hình và hệ thống điều hướng lệnh.
- **Giai đoạn 2**: Xây dựng hệ thống lưu trữ các lệnh đã phê duyệt và cơ chế kiểm soát tại Gateway.
- **Giai đoạn 3**: Cập nhật các Nút mạng để chúng có khả năng tự kiểm soát lệnh tại chỗ.
- **Giai đoạn 4**: Đồng bộ hóa các sự kiện thực thi lệnh vào nhật ký trò chuyện để người dùng theo dõi.

---
Tài liệu liên quan: [Công cụ thực thi lệnh](../../tools/exec.vi.md), [Phê duyệt lệnh](../../tools/exec-approvals.vi.md).
