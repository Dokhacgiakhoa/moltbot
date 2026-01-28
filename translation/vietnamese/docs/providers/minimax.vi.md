---
summary: "Sử dụng MiniMax M2.1 mạnh mẽ trong Moltbot"
read_when:
  - Bạn muốn dùng mô hình AI chuyên dụng cho doanh nghiệp và lập trình của MiniMax
---
# MiniMax

MiniMax là một công ty AI hàng đầu cung cấp dòng mô hình **M2/M2.1**. Phiên bản mới nhất **MiniMax M2.1** được xây dựng đặc biệt để xử lý các tác vụ thực tế phức tạp với khả năng lập trình vượt trội.

## Ưu điểm của mô hình M2.1:
- Khả năng **lập trình đa ngôn ngữ** cực mạnh (Rust, Java, Go, C++, JS/TS...).
- Xử lý các **chỉ dẫn phức tạp** lồng ghép vào nhau rất tốt, phù hợp cho quy trình làm việc văn phòng.
- Phản hồi **ngắn gọn, xúc tích** giúp tiết kiệm chi phí và tăng tốc độ xử lý.
- Tương thích tốt với các công cụ gọi hàm (Function calling).

## Cách thiết lập nhanh
Cách dễ nhất là sử dụng quy trình cấu hình tự động của Moltbot:
1. Chạy lệnh `moltbot configure`.
2. Chọn **Model/auth**.
3. Chọn **MiniMax M2.1**.
4. Nhập mã API Key của bạn (Lấy tại [minimax.io](https://minimax.io)).

## Ví dụ cấu hình thủ công:
```json5
{
  env: { MINIMAX_API_KEY: "sk-..." },
  agents: { defaults: { model: { primary: "minimax/MiniMax-M2.1" } } }
}
```

## Chế độ Lightning (Nhanh)
MiniMax cung cấp biến thể `MiniMax-M2.1-lightning` dành cho những ai cần tốc độ phản hồi cực nhanh. Hệ thống sẽ tự động điều phối giữa hai phiên bản tùy theo lưu lượng truy cập, nhưng bạn có thể chỉ định model Lightning nếu muốn ưu tiên tốc độ.

## Giải quyết sự cố
- **Lỗi Case-sensitive**: Hãy đảm bảo tên model được viết đúng chữ hoa chữ thường: `MiniMax-M2.1`.
- **Lỗi không nhận diện được model**: Nếu bot báo lỗi, hãy đảm bảo bạn đã cung cấp đúng mã API Key thông qua biến môi trường `MINIMAX_API_KEY`.

---
Tài liệu liên quan: [Hướng dẫn Gateway](../gateway/index.vi.md), [Lựa chọn mô hình AI](../../concepts/models.vi.md).
