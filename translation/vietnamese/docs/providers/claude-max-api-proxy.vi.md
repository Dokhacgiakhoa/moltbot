---
summary: "Sử dụng gói đăng ký Claude Max/Pro làm điểm cuối API tương thích với OpenAI"
read_when:
  - Bạn muốn tiết kiệm chi phí bằng cách dùng gói Subscription thay vì trả phí API theo token
---
# Claude Max API Proxy

**claude-max-api-proxy** là một công cụ cộng đồng giúp biến gói đăng ký Claude Max/Pro của bạn thành một điểm cuối API tương thích với chuẩn OpenAI. Điều này cho phép bạn sử dụng gói cước trả phí cố định hàng tháng của mình với bất kỳ công cụ nào hỗ trợ định dạng OpenAI.

## Tại sao nên dùng công cụ này?

| Cách thức | Chi phí | Phù hợp cho |
|----------|------|----------|
| Anthropic API | Trả theo token (Khá đắt đỏ cho Opus) | Ứng dụng sản xuất, lưu lượng lớn |
| Claude Max subscription | ~20$ (hoặc 200$ cho Max) cố định/tháng | Sử dụng cá nhân, lập trình viên |

Nếu bạn đã có gói đăng ký Claude và muốn tiết kiệm chi phí sử dụng API, bản proxy này là một giải pháp tuyệt vời.

## Cơ chế hoạt động

```
Ứng dụng của bạn → claude-max-api-proxy → Claude Code CLI → Anthropic (qua gói cá nhân)
   (Chuẩn OpenAI)          (Chuyển đổi định dạng)         (Dùng tài khoản đã đăng nhập)
```

Proxy này sẽ:
1. Nhận các yêu cầu chuẩn OpenAI tại địa chỉ `http://localhost:3456/v1/chat/completions`.
2. Chuyển đổi chúng thành các lệnh cho Claude Code CLI.
3. Trả về kết quả theo chuẩn OpenAI (hỗ trợ cả luồng tin nhắn - streaming).

## Cài đặt

```bash
# Yêu cầu Node.js 20+ và đã cài đặt Claude Code CLI
npm install -g claude-max-api-proxy

# Kiểm tra xem Claude CLI đã đăng nhập chưa
claude --version
```

## Cách sử dụng

### Khởi động máy chủ:
```bash
claude-max-api
# Máy chủ sẽ chạy tại http://localhost:3456
```

### Sử dụng với Moltbot:
Bạn có thể trỏ Moltbot tới bản proxy này như một nhà cung cấp OpenAI tùy chỉnh:

```json5
{
  env: {
    OPENAI_API_KEY: "không-cần-thiết",
    OPENAI_BASE_URL: "http://localhost:3456/v1"
  },
  agents: {
    defaults: {
      model: { primary: "openai/claude-opus-4" }
    }
  }
}
```

## Các mô hình hỗ trợ:
- `claude-opus-4`
- `claude-sonnet-4`
- `claude-haiku-4`

## Lưu ý quan trọng
- Đây là **công cụ cộng đồng**, không được hỗ trợ chính thức bởi Anthropic hay đội ngũ Moltbot.
- Proxy chạy trực tiếp trên máy của bạn và không gửi dữ liệu tới bất kỳ máy chủ trung gian nào khác.

---
Tài liệu liên quan: [Cấu hình Anthropic](./anthropic.vi.md), [Cấu hình OpenAI](./openai.vi.md).
