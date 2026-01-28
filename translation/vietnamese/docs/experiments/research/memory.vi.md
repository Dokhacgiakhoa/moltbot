---
summary: "Ghi chú nghiên cứu: Hệ thống ghi nhớ ngoại tuyến cho Moltbot (Sử dụng Markdown làm nguồn dữ liệu gốc)"
read_when:
  - Bạn muốn tìm hiểu cách Bot lưu trữ và truy xuất thông tin cá nhân của bạn
---

# Ghi nhớ không gian làm việc v2 (Nghiên cứu)

Mục tiêu: Xây dựng hệ thống ghi nhớ cho Bot (mặc định tại `~/clawd`), nơi các thông tin được lưu trữ dưới dạng các tệp Markdown hàng ngày (`memory/YYYY-MM-DD.md`) và các tệp ổn định như `memory.md`, `SOUL.md`.

Tài liệu này đề xuất một kiến trúc **ưu tiên ngoại tuyến (offline-first)**, giữ cho các tệp Markdown là nguồn dữ liệu gốc mà con người có thể đọc và sửa được, nhưng bổ sung thêm khả năng **truy xuất có cấu trúc** (tìm kiếm, tóm tắt thực thể) thông qua một mục lục dữ liệu được trích xuất.

## Tại sao cần thay đổi?
Hệ thống hiện tại (mỗi ngày một tệp) rất tốt cho việc ghi chép nhật ký, nhưng lại yếu trong việc:
- Truy xuất thông tin cũ nhanh chóng ("Lần trước chúng ta đã quyết định gì về X?").
- Tìm thông tin theo thực thể ("Hãy nói cho tôi biết về Anh Peter").
- Giải quyết các mẫu thuẫn thông tin theo thời gian.

## Các mục tiêu thiết kế
- **Ngoại tuyến (Offline)**: Hoạt động không cần mạng internet.
- **Dễ hiểu**: Các thông tin Bot tìm thấy phải chỉ rõ được nó nằm ở tệp nào, dòng bao nhiêu.
- **Thân thiện với AI**: Giúp AI dễ dàng lấy ra những mẩu tin nhỏ trong khi vẫn nằm trong giới hạn bộ nhớ của nó.

## Kiến trúc đề xuất

### 1. Kho lưu trữ dành cho con người
Giữ nguyên thư mục `~/clawd` để con người có thể đọc và sửa bằng tay:
```
~/clawd/
  memory.md          # Các sự thật quan trọng và sở thích lâu dài
  memory/
    2026-01-29.md    # Nhật ký hàng ngày (ghi chép tự do)
  bank/              # Các trang ghi nhớ đã được phân loại
    entities/        # Thông tin về từng người hoặc dự án cụ thể (ví dụ: Peter.md)
    opinions.md      # Các quan điểm và đánh giá của người dùng
```

### 2. Kho lưu trữ dành cho máy tính (Mục lục tìm kiếm)
Hệ thống sẽ tự động tạo một tệp mục lục (không cần lưu lên git) tại:
`~/clawd/.memory/index.sqlite`

Tệp này giúp Bot tìm kiếm văn bản cực nhanh (FTS5) và liên kết các thông tin lại với nhau mà không cần đọc lại toàn bộ hàng trăm tệp văn bản.

## Quy trình: Lưu giữ - Truy xuất - Suy ngẫm (Retain - Recall - Reflect)

### Lưu giữ (Retain)
Cuối mỗi ngày, Bot sẽ tự động thêm một phần `## Retain` vào nhật ký ngày hôm đó với các gạch đầu dòng ngắn gọn, chứa các sự thật đáng nhớ.

### Truy xuất (Recall)
Bot có thể tìm kiếm thông tin theo từ khóa, theo thời gian hoặc theo thực thể (người/vật). Kết quả trả về cho AI sẽ kèm theo nguồn trích dẫn rõ ràng.

### Suy ngẫm (Reflect)
Đây là một tác vụ định kỳ (ví dụ: mỗi tối hoặc khi Bot rảnh) để Bot tự tổng hợp lại các thông tin mới từ nhật ký hàng ngày vào các tệp tóm tắt lâu dài (như `bank/entities/Peter.md`).

---
Tài liệu liên quan: [Hệ thống Ghi nhớ (Memory)](../../concepts/memory.vi.md), [Nhật ký hàng ngày](../../automation/cron-jobs.vi.md).
