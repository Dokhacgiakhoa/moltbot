---
summary: "Tài liệu tham khảo lệnh `moltbot models` (Trạng thái/Danh sách/Thiết lập/Quét mô hình)"
read_when:
  - Bạn muốn thay đổi mô hình mặc định hoặc kiểm tra trạng thái xác thực của nhà cung cấp
---

# `moltbot models`

Lệnh này dùng để khám phá, quét và cấu hình các mô hình AI (mô hình mặc định, dự phòng, hồ sơ xác thực).

Tài liệu liên quan:
- Danh sách mô hình: [Mô hình AI](../providers/models.vi.md)
- Thiết lập ban đầu: [Bắt đầu nhanh](../../start/getting-started.vi.md)

## Các lệnh phổ biến

```bash
# Xem trạng thái các mô hình và xác thực hiện tại
moltbot models status

# Liệt kê tất cả các mô hình khả dụng
moltbot models list

# Đặt mô hình mặc định cho Agent
moltbot models set <tên-mô-hình-hoặc-alias>

# Quét các nhà cung cấp để tìm mô hình mới
moltbot models scan
```

## Chú ý về định dạng tên mô hình:
- Tên mô hình thường có dạng `nhà-cung-cấp/tên-model` (Ví dụ: `anthropic/claude-3-5-sonnet`).
- Nếu bạn sử dụng OpenRouter, hãy nhớ bao gồm cả tiền tố: `openrouter/anthropic/claude-3-5-sonnet`.
- Nếu bạn không ghi tên nhà cung cấp, Moltbot sẽ tìm trong danh sách các tên viết tắt (alias) hoặc dùng nhà cung cấp mặc định.

## Quản lý xác thực (Auth profiles)
Bạn có thể quản lý cách Moltbot đăng nhập vào các nền tảng AI:
```bash
moltbot models auth add          # Thêm tài khoản mới qua hướng dẫn
moltbot models auth login        # Đăng nhập vào một nhà cung cấp cụ thể
moltbot models auth setup-token  # Cấu hình bằng mã Token (đối với Anthropic)
```

---
Tài liệu liên quan: [Lựa chọn mô hình](../../concepts/models.vi.md), [Hạn mức sử dụng](../../concepts/usage-tracking.md).
