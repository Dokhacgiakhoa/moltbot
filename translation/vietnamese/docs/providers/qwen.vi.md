---
summary: "Sử dụng các mô hình Qwen miễn phí (OAuth) trong Moltbot"
read_when:
  - Bạn muốn dùng mô hình Qwen Coder hoặc Qwen Vision mà không cần tạo API key
---
# Qwen (Alibaba Cloud)

Qwen cung cấp một luồng đăng nhập nhanh (OAuth) cho phép bạn sử dụng miễn phí các mô hình **Qwen Coder** và **Qwen Vision** (Hỗ trợ tối đa 2,000 yêu cầu/ngày).

## Cách kích hoạt
1. **Bật plugin xác thực**:
   ```bash
   moltbot plugins enable qwen-portal-auth
   ```
   Sau đó hãy khởi động lại Gateway.

2. **Đăng nhập**:
   ```bash
   moltbot models auth login --provider qwen-portal --set-default
   ```
   Lệnh này sẽ hiển thị một mã số và đường dẫn để bạn đăng nhập tài khoản Alibaba Cloud.

## Các mô hình khả dụng:
- `qwen-portal/coder-model`: Chuyên dùng cho lập trình và logic.
- `qwen-portal/vision-model`: Có khả năng nhìn và phân tích hình ảnh.

## Lưu ý quan trọng
- Nếu bạn đã từng đăng nhập qua **Qwen Code CLI** trên máy tính, Moltbot sẽ tự động đồng bộ mã đăng nhập đó.
- Mã đăng nhập sẽ tự động làm mới (auto-refresh). Nếu bot báo lỗi không thể truy cập, hãy chạy lại lệnh đăng nhập ở bước 2.

---
Tài liệu liên quan: [AI từ Trung Quốc](./index.vi.md), [Hệ thống Plugin](../../plugin.vi.md).
