---
summary: "Hướng dẫn chạy các bài kiểm tra lỗi (tests) tại máy cục bộ và các chế độ đo lường hiệu năng"
read_when:
  - Bạn đang thực hiện viết mã mới hoặc sửa lỗi và cần kiểm tra tính ổn định của mã nguồn
---

# Kiểm thử (Tests)

Đây là các lệnh hỗ trợ kiểm tra tính đúng đắn của mã nguồn Moltbot.

## Các lệnh chính
- **`pnpm test:force`**: Dọn dẹp các tiến trình Gateway cũ đang chiếm cổng và chạy toàn bộ bộ kiểm thử Vitest trong môi trường cách ly.
- **`pnpm test:coverage`**: Chạy kiểm thử và đo lường độ phủ của mã nguồn. Ngưỡng tối thiểu được thiết lập là 70% cho toàn dự án.
- **`pnpm test:e2e`**: Kiểm tra các kịch bản thực tế (End-to-End) như kết nối WebSocket, HTTP và ghép nối các nút mạng.
- **`pnpm test:live`**: Kiểm tra kết nối trực tiếp với các nhà cung cấp AI (yêu cầu bạn phải có sẵn API Keys và bật cờ `LIVE=1`).

## Đo lường độ trễ (Latency Bench)
Bạn có thể đo tốc độ phản hồi của các mô hình AI khác nhau bằng kịch bản:
`scripts/bench-model.ts`

**Kết quả tham khảo (cuối năm 2025):**
- **Minimax**: Tốc độ trung bình khoảng 1.2 giây.
- **Claude Opus**: Tốc độ trung bình khoảng 2.4 giây.

## Kiểm tra cài đặt bằng Docker
Nếu bạn muốn giả lập quy trình cài đặt Moltbot từ đầu trên một máy Linux sạch, hãy sử dụng:
`scripts/e2e/onboard-docker.sh`

Kịch bản này sẽ tạo một container Docker, chạy cài đặt qua lệnh `curl`, thiết lập các thông số ban đầu và kiểm tra xem Bot có hoạt động tốt không.

---
Tài liệu liên quan: [Phát hành bản dựng](./RELEASING.vi.md), [Thiết lập nhà phát triển](../platforms/mac/dev-setup.vi.md).
