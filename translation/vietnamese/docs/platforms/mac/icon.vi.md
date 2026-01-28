---
summary: "Các trạng thái và hoạt ảnh của biểu tượng thanh menu cho Moltbot trên macOS"
read_when:
  - Bạn muốn thay đổi hành vi hiển thị của biểu tượng trên thanh menu
---

# Trạng thái biểu tượng thanh Menu (Icon States)

Moltbot sử dụng một biểu tượng linh hoạt trên thanh menu để thể hiện trạng thái hoạt động của Bot:

- **Chờ (Idle)**: Biểu tượng hoạt hình bình thường (chớp mắt, thỉnh thoảng cử động nhẹ).
- **Tạm dừng (Paused)**: Biểu tượng ở trạng thái mờ (`appearsDisabled`) và không có chuyển động.
- **Kích hoạt giọng nói (Tai to)**: Khi nghe thấy từ khóa đánh thức, tai của biểu tượng sẽ to lên (gấp 1.9 lần) để báo hiệu đang lắng nghe. Sau 1 giây im lặng, tai sẽ thu nhỏ lại về mức bình thường.
- **Đang làm việc (Agent running)**: Khi Bot đang xử lý yêu cầu, chân của biểu tượng sẽ cử động nhanh hơn để báo hiệu đang "chạy việc".

## Lưu ý về thiết kế
- Kích thước gốc là 18x18 pt, được vẽ thông qua bộ dựng hình `CritterIconRenderer`.
- Các trạng thái chuyển đổi hoạt ảnh được thiết lập với thời gian chờ (TTL) ngắn (thường dưới 10 giây) để biểu tượng nhanh chóng trở về trạng thái bình thường nếu công việc bị treo.

---
Tài liệu liên quan: [Logic trạng thái thanh menu](./menu-bar.vi.md), [Thiết lập nhà phát triển](./dev-setup.vi.md).
