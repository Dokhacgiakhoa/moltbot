---
summary: "Chạy Moltbot Gateway 24/7 trên máy ảo Google Cloud Compute Engine (Docker)"
read_when:
  - Bạn muốn sử dụng cơ sở hạ tầng của Google Cloud để chạy Bot
  - Bạn muốn tận dụng gói miễn phí e2-micro của GCP
---

# Moltbot trên Google Cloud (GCP)

Bạn có thể chạy Moltbot Gateway trên một máy ảo **Compute Engine** của Google Cloud. Đây là phương án rất ổn định, đặc biệt là nếu bạn đã có sẵn tài khoản GCP.

## Các bước thực hiện nhanh

1. **Tạo dự án**: Tạo một dự án mới trên Google Cloud Console.
2. **Tạo máy ảo (VM)**:
   - Khuyên dùng: Loại máy `e2-small` (2 vCPU, 2GB RAM) cho hiệu suất ổn định.
   - Tiết kiệm: Loại máy `e2-micro` (nằm trong gói miễn phí của GCP nhưng có thể bị lag khi Agent xử lý nặng).
3. **Cài đặt Docker**: Cài đặt Docker bên trong máy ảo Debian/Ubuntu.
4. **Khởi chạy Bot**: Tải mã nguồn Moltbot và chạy bằng Docker Compose tương tự như hướng dẫn cho Hetzner.

## Truy cập an toàn (SSH Tunnel)

Thay vì mở cổng 18789 công khai trên internet, bạn nên sử dụng lệnh `gcloud` để tạo đường truyền an toàn từ máy tính của mình:

```bash
gcloud compute ssh moltbot-gateway --zone=us-central1-a -- -L 18789:127.0.0.1:18789
```

Sau khi chạy lệnh trên, bạn có thể mở `http://127.0.0.1:18789` trên trình duyệt máy mình để sử dụng Bot đang chạy trên Google Cloud.

## Lưu ý về chi phí
GCP có gói "Always Free" cho máy ảo `e2-micro` ở một số khu vực (như `us-central1`). Tuy nhiên, hãy theo dõi bộ nhớ (RAM) vì Agent có thể tiêu tốn nhiều RAM khi thực hiện các tác vụ phức tạp.

---
Tài liệu liên quan: [Hướng dẫn Hetzner](./hetzner.vi.md), [Cài đặt Docker](../../install/docker.vi.md).
