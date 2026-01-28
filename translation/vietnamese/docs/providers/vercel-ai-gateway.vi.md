---
title: "Vercel AI Gateway"
summary: "Thiết lập Vercel AI Gateway (xác thực và chọn mô hình)"
read_when:
  - Bạn muốn sử dụng Vercel AI Gateway làm cổng kết nối trung tâm cho các AI của mình
---
# Vercel AI Gateway

[Vercel AI Gateway](https://vercel.com/ai-gateway) cung cấp một API hợp nhất giúp bạn truy cập vào hàng trăm mô hình thông qua một điểm kết nối duy nhất.

- **Nhà cung cấp**: `vercel-ai-gateway`
- **Xác thực**: Sử dụng biến môi trường `AI_GATEWAY_API_KEY`.
- **Chuẩn API**: Tương thích với chuẩn tin nhắn của Anthropic.

## Khởi động nhanh

1. **Cung cấp API Key**:
   ```bash
   moltbot onboard --auth-choice ai-gateway-api-key
   ```

2. **Thiết lập mô hình mặc định**:
   ```json5
   {
     agents: {
       defaults: {
         model: { primary: "vercel-ai-gateway/anthropic/claude-opus-4.5" }
       }
     }
   }
   ```

## Ghi chú về môi trường
Nếu bạn chạy Moltbot dưới dạng dịch vụ chạy ngầm (daemon), hãy đảm bảo rằng biến `AI_GATEWAY_API_KEY` đã được khai báo và có thể truy cập được bởi tiến trình đó (Ví dụ: đặt trong file `.env` tại thư mục cấu hình của Moltbot).

---
Tài liệu liên quan: [Hướng dẫn Onboarding](../../start/onboarding.vi.md), [Toàn bộ nhà cung cấp](./index.vi.md).
