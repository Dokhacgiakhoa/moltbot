---
summary: "Nơi Moltbot tải các biến môi trường và thứ tự ưu tiên của chúng"
---
# Biến môi trường (Environment variables)

Moltbot lấy các biến môi trường từ nhiều nguồn khác nhau. Quy tắc chung là **không bao giờ ghi đè các giá trị hiện có**.

## Thứ tự ưu tiên (Cao nhất → Thấp nhất)

1. **Tiền trình hiện tại (Process environment)**: Các biến mà tiến trình Gateway đã có sẵn từ bảng điều khiển (shell) hoặc dịch vụ chạy ngầm (daemon).
2. **Tệp `.env` trong thư mục làm việc hiện tại**: Tải mặc định qua dotenv; không ghi đè giá trị đã có.
3. **Tệp `.env` toàn cục**: Tại đường dẫn `~/.clawdbot/.env` (hoặc `$CLAWDBOT_STATE_DIR/.env`); không ghi đè giá trị đã có.
4. **Khối cấu hình `env`** trong tệp `~/.clawdbot/moltbot.json`: Chỉ áp dụng nếu biến đó chưa có giá trị.
5. **Nhập từ bảng điều khiển đăng nhập (Shell import)**: (Nếu bật `CLAWDBOT_LOAD_SHELL_ENV=1`), chỉ áp dụng cho các khóa còn thiếu.

## Khối cấu hình `env`

Có hai cách tương đương để đặt các biến môi trường ngay trong tệp cấu hình:

```json
{
  "env": {
    "OPENROUTER_API_KEY": "sk-or-...",
    "vars": {
      "GROQ_API_KEY": "gsk-..."
    }
  }
}
```

## Nhập biến từ Shell

Khi chế độ `env.shellEnv` được bật, hệ thống sẽ chạy bảng điều khiển (shell) của bạn và chỉ nhập các khóa **còn thiếu**:

```json
{
  "env": {
    "shellEnv": {
      "enabled": true,
      "timeoutMs": 15000
    }
  }
}
```

## Thay thế biến môi trường trong cấu hình

Bạn có thể tham chiếu trực tiếp các biến môi trường trong các giá trị chuỗi của tệp cấu hình bằng cú pháp `${TÊN_BIẾN}`:

```json
{
  "models": {
    "providers": {
      "vercel-gateway": {
        "apiKey": "${VERCEL_GATEWAY_API_KEY}"
      }
    }
  }
}
```

---
Tài liệu liên quan: [Cấu hình Gateway](../../gateway/configuration.vi.md), [Câu hỏi thường gặp về biến môi trường](../../help/faq.vi.md#env-vars-and-env-loading).
