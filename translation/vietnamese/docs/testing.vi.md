---
summary: "Bộ công cụ kiểm thử: Suite unit/e2e/live, Docker runners và phạm vi bao phủ của từng bài kiểm tra"
---

# Kiểm thử (Testing)

Moltbot sử dụng ba bộ công cụ kiểm thử trên nền tảng Vitest (Unit/Integration, E2E, Live) cùng với một số trình chạy trên Docker.

Tài liệu này là hướng dẫn về "cách chúng tôi kiểm thử":
- Phạm vi của từng bộ suite (và những gì nó bỏ qua).
- Các lệnh cần chạy cho quy trình làm việc thông thường.
- Cách các bài kiểm tra trực tiếp (Live tests) sử dụng thông tin xác thực.
- Cách bổ sung các bài kiểm tra lỗi hồi quy (regression) cho các vấn đề thực tế của nhà cung cấp AI.

## Bắt đầu nhanh

Hàng ngày:
- Kiểm tra toàn bộ (trước khi push): `pnpm lint && pnpm build && pnpm test`

Khi bạn thay đổi nhiều và cần sự tin cậy:
- Kiểm tra độ bao phủ (coverage): `pnpm test:coverage`
- Kiểm tra E2E: `pnpm test:e2e`

Khi gỡ lỗi với các nhà cung cấp/mô hình thực tế (yêu cầu API key thực):
- Kiểm tra trực tiếp (Live suite): `pnpm test:live`

## Các bộ suite kiểm thử

### 1. Unit / Integration (Mặc định)
- Lệnh: `pnpm test`
- Phạm vi: Các bài kiểm tra đơn vị (unit) và tích hợp trong quy trình (xác thực gateway, điều hướng, công cụ, cấu hình).
- Đặc điểm: Chạy trong CI, không cần API key thực, nhanh và ổn định.

### 2. E2E (Kiểm tra khói Gateway)
- Lệnh: `pnpm test:e2e`
- Phạm vi: Hành vi đầu-cuối của đa thực thể Gateway, WebSocket, ghép nối nút mạng.
- Đặc điểm: Chạy trong CI, không cần API key thực.

### 3. Live (Nhà cung cấp & Mô hình thực tế)
- Lệnh: `pnpm test:live`
- Phạm vi: Kiểm tra xem nhà cung cấp/mô hình có thực sự hoạt động *ngay bây giờ* với API key thực hay không. Phát hiện sự thay đổi định dạng của nhà cung cấp, lỗi gọi công cụ (tool calling), hoặc giới hạn băng thông.
- Đặc điểm: Tốn phí (Token), chịu ảnh hưởng bởi đường truyền mạng, khuyên dùng khi cần kiểm tra cụ thể một mô hình nào đó.

## Kiểm tra trực tiếp: Model Smoke

Được chia làm hai lớp để cô lập lỗi:
- **Lớp 1 (Direct model)**: Kiểm tra xem mô hình có trả lời được không với API key đã cho (không qua Gateway).
- **Lớp 2 (Gateway smoke)**: Kiểm tra toàn bộ quy trình từ Gateway + Agent + Mô hình (phiên làm việc, lịch sử, công cụ, hộp cát).

## Kiểm tra với Docker (Tùy chọn)

Dùng để kiểm tra xem hệ thống có "chạy tốt trên Linux" hay không bằng cách gắn các thư mục cấu hình và không gian làm việc cục bộ vào container:
- `pnpm test:docker:live-models`
- `pnpm test:docker:live-gateway`

## Hướng dẫn bổ sung bài kiểm tra lỗi hồi quy (Regressions)

Khi bạn sửa một lỗi phát sinh từ thực tế:
- Nếu có thể, hãy thêm một bài kiểm tra hồi quy an toàn cho CI (sử dụng mock/stub).
- Nếu lỗi chỉ xuất hiện khi chạy thực tế (như lỗi xác thực của nhà cung cấp), hãy giữ bài kiểm tra đó trong bộ suite Live và bật/tắt qua biến môi trường.

---
Tài liệu liên quan: [Ghi nhật ký](./logging.vi.md), [Xử lý sự cố](./help/troubleshooting.vi.md).
