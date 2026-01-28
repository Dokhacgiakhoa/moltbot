---
summary: "Sử dụng OpenAI qua API key hoặc gói đăng ký Codex trong Moltbot"
read_when:
  - Bạn muốn sử dụng các mô hình GPT của OpenAI trong Moltbot
---
# OpenAI

OpenAI cung cấp các API dành cho nhà phát triển để truy cập vào dòng mô hình GPT. Moltbot hỗ trợ cả hình thức sử dụng mã **API key** truyền thống và đăng nhập thông qua gói **Codex/ChatGPT subscription**.

## Lựa chọn A: Sử dụng OpenAI API key
**Phù hợp nhất cho**: Truy cập trực tiếp qua API và trả phí theo dung lượng thực tế.
Bạn lấy mã API key từ bảng điều khiển của OpenAI Platform.

### Thiết lập nhanh:
```bash
moltbot onboard --auth-choice openai-api-key
# Hoặc truyền nhanh qua biến môi trường
moltbot onboard --openai-api-key "$OPENAI_API_KEY"
```

## Lựa chọn B: Sử dụng gói đăng ký Codex/Subscription
**Phù hợp nhất cho**: Tận dụng quyền lợi từ gói trả phí ChatGPT/Codex của bạn thay vì trả tiền theo từng câu lệnh.

### Thiết lập:
```bash
# Chạy quy trình đăng nhập OAuth trong wizard
moltbot onboard --auth-choice openai-codex

# Hoặc chạy lệnh đăng nhập trực tiếp
moltbot models auth login --provider openai-codex
```

## Ghi chú quan trọng
- Khi chỉ định model, hãy luôn dùng định dạng `nhà_cung_cấp/tên_model` (Ví dụ: `openai/gpt-4o`).
- Các chi tiết về cách Moltbot quản lý mã xác thực có thể xem tại phần tài liệu về OAuth.

---
Tài liệu liên quan: [Khái niệm mô hình AI](../../concepts/models.vi.md), [Xác thực OAuth](../../concepts/oauth.vi.md).
