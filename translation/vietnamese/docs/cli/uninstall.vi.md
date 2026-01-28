---
summary: "Tài liệu tham khảo lệnh `moltbot uninstall` (Gỡ bỏ dịch vụ gateway và dữ liệu cục bộ)"
read_when:
  - Bạn muốn gỡ bỏ hoàn toàn Moltbot khỏi hệ thống của mình
---

# `moltbot uninstall`

Lệnh này dùng để gỡ bỏ dịch vụ Gateway và các dữ liệu cấu hình cục bộ. Lưu ý lệnh này chỉ gỡ bỏ các thành phần vận hành, bộ công cụ CLI (lệnh `moltbot`) vẫn sẽ được giữ lại trừ khi bạn gỡ cài đặt qua npm/pnpm.

## Ví dụ sử dụng

```bash
# Gỡ bỏ có xác nhận từ người dùng
moltbot uninstall

# Gỡ bỏ tất cả dữ liệu và bỏ qua các câu hỏi xác nhận
moltbot uninstall --all --yes

# Chạy thử để xem những gì sẽ bị xóa (không xóa thật)
moltbot uninstall --dry-run
```

Tài liệu liên quan:
- [Cài đặt hệ thống](../../install/docker.md).
