---
summary: "Tài liệu tham khảo lệnh `moltbot update` (Cập nhật hệ thống an toàn + tự động khởi động lại gateway)"
read_when:
  - Bạn muốn cập nhật Moltbot lên phiên bản mới nhất một cách an toàn
  - Bạn muốn chuyển đổi giữa các kênh phát hành (stable/beta/dev)
---

# `moltbot update`

Lệnh này giúp cập nhật Moltbot một cách an toàn và cho phép bạn chuyển đổi linh hoạt giữa các kênh phát hành: Chính thức (stable), Thử nghiệm (beta) hoặc Phát triển (dev).

## Ví dụ sử dụng

```bash
# Kiểm tra và cập nhật lên phiên bản mới nhất
moltbot update

# Chỉ kiểm tra trạng thái cập nhật mà không thực hiện
moltbot update status

# Chuyển sang kênh dùng thử (beta)
moltbot update --channel beta

# Cập nhật nhưng không tự động khởi động lại Gateway
moltbot update --no-restart
```

## Các kênh cập nhật (Channels)
- **stable**: Phiên bản chính thức, ổn định nhất cho túi tiền và hệ thống của bạn.
- **beta**: Các tính năng mới đang trong quá trình hoàn thiện.
- **dev**: Phiên bản mới nhất trực tiếp từ nhánh phát triển (thường dành cho cộng tác viên hoặc những người muốn trải nghiệm sớm nhất).

## Các bước hệ thống thực hiện:
1. Kiểm tra phiên bản hiện tại và so sánh với máy chủ.
2. Tải về và cài đặt các phụ thuộc mới (dependencies).
3. Biên dịch lại các thành phần hệ thống và giao diện điều khiển.
4. Chạy lệnh `moltbot doctor` để đảm bảo sau khi cập nhật hệ thống vẫn hoạt động tốt.
5. Tự động khởi động lại Gateway để áp dụng các thay đổi (trừ khi bạn dùng cờ `--no-restart`).

---
Tài liệu liên quan: [Hướng dẫn cập nhật chi tiết](../../install/updating.md), [Chẩn đoán hệ thống](./doctor.vi.md).
