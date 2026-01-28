---
summary: "Cách Moltbot luân chuyển các hồ sơ xác thực và dự phòng lỗi giữa các mô hình AI"
read_when:
  - Bạn muốn chẩn đoán lỗi luân chuyển hồ sơ, thời gian chờ hoặc hành vi dự phòng của mô hình
---

# Dự phòng lỗi mô hình (Failover)

Moltbot xử lý các lỗi xảy ra theo hai giai đoạn:
1) **Luân chuyển hồ sơ xác thực**: Thử các tài khoản/khóa API khác nhau trong cùng một nhà cung cấp.
2) **Dự phòng mô hình**: Chuyển sang mô hình tiếp theo trong danh sách `fallbacks` nếu nhà cung cấp hiện tại gặp sự cố hoàn toàn.

## Hồ sơ xác thực (Auth Profiles)

Moltbot sử dụng các **hồ sơ xác thực** cho cả khóa API và token OAuth.
- Các bí mật được lưu tại `~/.clawdbot/agents/<agentId>/agent/auth-profiles.json`.
- Các loại định danh: `api_key` (Khóa API) và `oauth` (Đăng nhập qua Google/Github/v.v.).

## Thứ tự luân chuyển

Khi một nhà cung cấp có nhiều hồ sơ xác thực, Moltbot sẽ chọn theo thứ tự:
1. **Theo cấu hình cụ thể**: Tham số `auth.order`.
2. **Loại hồ sơ**: Luôn ưu tiên **OAuth trước Khóa API**.
3. **Thống kê sử dụng**: Hồ sơ nào lâu chưa dùng nhất sẽ được ưu tiên đưa lên đầu.
4. **Hồ sơ bị lỗi/vô hiệu hóa** sẽ bị đẩy xuống cuối danh sách.

## Thời gian chờ (Cooldowns)

Khi một hồ sơ bị lỗi (lỗi xác thực, giới hạn băng thông - rate limit), Moltbot sẽ đưa nó vào trạng thái chờ và chuyển sang hồ sơ tiếp theo. Thời gian chờ sẽ tăng dần theo lũy kế (1 phút, 5 phút, 25 phút, tối đa 1 giờ).

## Vô hiệu hóa do thanh toán

Nếu gặp lỗi liên quan đến tài chính (như "hết tiền trong tài khoản" - insufficient credits), Moltbot sẽ coi đây là lỗi nghiêm trọng. Thay vì chỉ chờ một lát, hồ sơ đó sẽ bị **vô hiệu hóa** trong một khoảng thời gian dài (mặc định bắt đầu từ 5 giờ) trước khi hệ thống thử lại.

---
Tài liệu liên quan: [Xác thực OAuth](./oauth.vi.md), [Quản lý mô hình](./models.vi.md).
