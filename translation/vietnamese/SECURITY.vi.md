# Chính sách Bảo mật (Security Policy)

Nếu bạn tin rằng mình đã phát hiện ra lỗ hổng bảo mật trong Moltbot, xin hãy báo cáo một cách riêng tư (private).

## Cách báo cáo

- **Email:** `steipete@gmail.com`
- **Nội dung cần có:**
  - Các bước tái hiện lỗi (reproduction steps).
  - Đánh giá mức độ ảnh hưởng (impact assessment).
  - Nếu có thể, hãy kèm theo một PoC (Proof of Concept) tối giản.

## Hướng dẫn Vận hành An toàn

Để hiểu rõ về mô hình các mối đe dọa (threat model) và cách gia cố hệ thống (hardening), bao gồm việc dùng lệnh `moltbot security audit --deep` và `--fix`, vui lòng xem tại:

👉 [Tài liệu Bảo mật Gateway](https://docs.molt.bot/gateway/security)

### Lưu ý về Giao diện Web (Web Interface)

Giao diện web của Moltbot được thiết kế để **chỉ sử dụng nội bộ (local use only)**.
Tuyệt đối **KHÔNG** mở (bind) giao diện này ra internet công cộng trực tiếp. Nó chưa được gia cố để chống chọi với môi trường internet đầy rẫy rủi ro.

## Yêu cầu Môi trường chạy (Runtime Requirements)

### Phiên bản Node.js

Moltbot yêu cầu **Node.js 22.12.0 trở lên** (bản LTS). Phiên bản này cực kỳ quan trọng vì nó chứa các bản vá bảo mật cốt lõi:

- **CVE-2025-59466:** Lỗ hổng từ chối dịch vụ (DoS) liên quan đến `async_hooks`.
- **CVE-2026-21636:** Lỗ hổng cho phép vượt qua mô hình phân quyền (Permission model bypass).

Hãy kiểm tra phiên bản Node.js của bạn:

```bash
node --version  # Kết quả phải là v22.12.0 trở lên
```

### Bảo mật Docker

Nếu bạn chạy Moltbot trong Docker, hãy tuân thủ các nguyên tắc sau:

1.  **Chạy non-root:** Image chính thức đã được cấu hình để chạy dưới user `node` thay vì `root` để giảm thiểu rủi ro bị tấn công leo thang đặc quyền.
2.  **Read-only:** Sử dụng cờ `--read-only` bất cứ khi nào có thể để ngăn chặn việc ghi đè lên hệ thống file của container.
3.  **Hạn chế quyền:** Dùng `--cap-drop=ALL` để tước bỏ các quyền Linux capabilities không cần thiết.

**Ví dụ lệnh chạy Docker an toàn:**

```bash
docker run --read-only --cap-drop=ALL \
  -v moltbot-data:/app/data \
  moltbot/moltbot:latest
```

## Quét lỗ hổng (Security Scanning)

Dự án này sử dụng công cụ `detect-secrets` để tự động phát hiện các thông tin nhạy cảm (API keys, passwords...) trong quá trình CI/CD.
- Cấu hình: xem file `.detect-secrets.cfg`.
- Baseline (dữ liệu mẫu): xem file `.secrets.baseline`.

**Cách chạy quét thủ công (local):**

```bash
pip install detect-secrets==1.5.0
detect-secrets scan --baseline .secrets.baseline
```
