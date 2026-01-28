---
summary: "Tài liệu tham khảo lệnh `moltbot security` (Kiểm toán và khắc phục các lỗ hổng bảo mật phổ biến)"
read_when:
  - Bạn muốn thực hiện kiểm tra bảo mật nhanh cho cấu hình và trạng thái hệ thống
---

# `moltbot security`

Các công cụ bảo mật dùng để kiểm tra (audit) và đưa ra các đề xuất sửa chữa (fix).

Tài liệu liên quan:
- Hướng dẫn bảo mật: [Security](../gateway/security/index.vi.md)

## Kiểm toán (Audit)

```bash
# Chạy kiểm tra bảo mật cơ bản
moltbot security audit

# Kiểm tra sâu và chi tiết hơn
moltbot security audit --deep

# Tự động thực hiện các bước sửa lỗi an toàn (như phân quyền file, v.v.)
moltbot security audit --fix
```

## Các hạng mục kiểm tra chính:
- **Phạm vi phiên làm việc (Session Scope)**: Cảnh báo nếu nhiều người cùng gửi tin nhắn trực tiếp (DM) vào một phiên làm việc chung, có thể gây rò rỉ dữ liệu giữa các người dùng. Hệ thống sẽ khuyên dùng chế độ `per-channel-peer`.
- **Sandboxing**: Cảnh báo nếu bạn sử dụng các mô hình nhỏ (dưới 300 tỷ tham số) dễ bị tấn công tấn công prompt injection mà không bật chế độ sandbox khi dùng các công cụ trình duyệt/web.

---
Tài liệu liên quan: [Môi trường cô lập](./sandbox.vi.md).
