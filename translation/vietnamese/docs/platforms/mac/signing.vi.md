---
summary: "Quy trình ký tên (Signing) cho các bản dựng thử nghiệm trên macOS"
read_when:
  - Bạn đang biên dịch ứng dụng macOS và gặp lỗi về quyền hạn hoặc chữ ký
---

# Ký tên ứng dụng macOS (Bản dựng thử nghiệm)

Để duy trì các quyền hạn bảo mật (như ghi màn hình, micro) sau mỗi lần biên dịch lại mã nguồn, ứng dụng macOS cần được ký tên bằng một danh tính ổn định.

## Quy trình đóng gói
Chúng tôi sử dụng kịch bản `scripts/package-mac-app.sh` để thực hiện:
- Thiết lập định danh ổn định: `bot.molt.mac.debug`.
- Ký tên chính thức cho tệp thực thi chính và các thành phần đi kèm.
- Nhúng các thông tin về thời gian xây dựng (Timestamp) và mã commit Git để hiển thị trong phần **About**.

## Sử dụng
Bạn có thể chỉ định danh tính ký tên thông qua biến môi trường:

```bash
# Ký tên bằng chứng chỉ Apple Development của bạn (Khuyên dùng)
SIGN_IDENTITY="Apple Development: Ten Cua Ban" scripts/package-mac-app.sh

# Ký tên tạm thời (ad-hoc) - Quyền hạn sẽ bị mất mỗi khi build lại
ALLOW_ADHOC_SIGNING=1 scripts/package-mac-app.sh
```

## Tại sao việc ký tên lại quan trọng?
Hệ thống bảo mật macOS (TCC) sẽ "quên" các quyền bạn đã cấp (như cho phép dùng Micro) nếu nó phát hiện chữ ký của ứng dụng thay đổi. Việc ký tên giúp macOS nhận diện đây vẫn là cùng một ứng dụng tin cậy từ lần trước.

---
Tài liệu liên quan: [Quyền hạn trên macOS](./permissions.vi.md), [Thiết lập nhà phát triển](./dev-setup.vi.md).
