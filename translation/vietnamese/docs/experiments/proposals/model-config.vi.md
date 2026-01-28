---
summary: "Tìm tòi: Cấu hình mô hình, hồ sơ xác thực và hành vi dự phòng khi lỗi"
read_when:
  - Bạn đang tìm hiểu các ý tưởng về cách chọn mô hình và xác thực trong tương lai
---

# Cấu hình Mô hình (Tìm hiểu)

Tài liệu này ghi lại các **ý tưởng** cho việc cấu hình mô hình AI trong tương lai. Đây chưa phải là tài liệu hướng dẫn sử dụng chính thức. Để xem các tính năng hiện đang hoạt động, hãy tham khảo:
- [Các mô hình AI](../../concepts/models.vi.md)
- [Cơ chế dự phòng khi lỗi (Failover)](../../concepts/model-failover.vi.md)

## Động lực thay đổi
Người dùng mong muốn:
- Có nhiều hồ sơ xác thực (auth profiles) cho cùng một nhà cung cấp (ví dụ: tài khoản cá nhân và tài khoản công việc).
- Việc chọn mô hình đơn giản hơn với các cơ chế dự phòng có thể dự đoán được.
- Phân biệt rõ ràng giữa các mô hình chỉ có văn bản và các mô hình có khả năng xử lý hình ảnh.

## Hướng đi tiềm năng
- Giữ việc chọn mô hình đơn giản: sử dụng định dạng `nhà_cung_cấp/mô_hình` hoặc các tên gợi nhớ (aliases).
- Cho phép mỗi nhà cung cấp có nhiều hồ sơ xác thực với thứ tự ưu tiên rõ ràng.
- Sử dụng một danh sách dự phòng toàn cầu để mọi cuộc trò chuyện đều hoạt động ổn định khi có lỗi xảy ra.

## Các câu hỏi chưa có lời giải
- Việc xoay vòng hồ sơ xác thực nên thực hiện theo từng nhà cung cấp hay theo từng mô hình cụ thể?
- Làm thế nào để giao diện người dùng hiển thị việc chọn hồ sơ xác thực cho một phiên làm việc một cách dễ hiểu nhất?
- Cách an toàn nhất để chuyển đổi từ cấu hình cũ sang hệ thống mới là gì?

---
Tài liệu liên quan: [Xác thực mô hình](../../concepts/oauth.vi.md).
