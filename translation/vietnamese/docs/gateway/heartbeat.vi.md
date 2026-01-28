---
summary: "Cấu hình tin nhắn Nhịp tim và quy tắc thông báo định kỳ của Agent"
read_when:
  - Bạn muốn Agent tự động kiểm tra và nhắc nhở công việc định kỳ
---

# Nhịp tim (Heartbeat - Gateway)

Nhịp tim (Heartbeat) thực hiện các **lượt chạy định kỳ** của Agent trong phiên hội thoại chính để AI có thể tự động đưa ra các thông báo cần thiết mà không cần bạn phải nhắn tin trước.

## Bắt đầu nhanh
1. Mặc định tính năng này được bật mỗi **30 phút** (hoặc 1 tiếng tùy mô hình).
2. Tạo một tệp `HEARTBEAT.md` trong thư mục làm việc của Agent để liệt kê các việc cần AI kiểm tra định kỳ (ví dụ: "Kiểm tra email mới", "Nhắc tôi uống nước").
3. Bạn có thể giới hạn thời gian hoạt động của nhịp tim để tránh bị làm phiền vào ban đêm.

**Ví dụ cấu hình:**
```json5
{
  "agents": {
    "defaults": {
      "heartbeat": {
        "every": "30m",
        "target": "last", // Gửi đến kênh nhắn tin cuối cùng bạn đã dùng
        "activeHours": { "start": "08:00", "end": "22:00" }
      }
    }
  }
}
```

## Thỏa thuận phản hồi (Response Contract)
Để Tiết kiệm chi phí và tránh làm phiền, Agent tuân thủ quy tắc sau:
- Nếu sau khi kiểm tra, Agent thấy **không có gì cần chú ý**, nó sẽ trả về mã **`HEARTBEAT_OK`**. Moltbot sẽ ghi nhận và **không gửi** tin nhắn này đến điện thoại của bạn.
- Nếu có việc cần báo cáo, Agent sẽ viết nội dung cảnh báo (không chứa từ khóa trên). Moltbot sẽ gửi tin nhắn này ngay lập tức.

## Tệp HEARTBEAT.md
Đây là tệp tin quan trọng nhất để điều khiển hành vi của AI. Hãy coi nó như một danh sách các đầu mục công việc mà bạn giao cho AI kiểm tra mỗi 30 phút. 

**Mẹo nhỏ**: Bạn có thể yêu cầu Agent (trong ô chat bình thường) tự cập nhật tệp `HEARTBEAT.md` này cho mình: *"Này, từ giờ hãy thêm mục kiểm tra giá Bitcoin vào danh sách nhịp tim của tôi nhé"*.

## Lưu ý về chi phí
Mỗi lượt chạy Nhịp tim tương đương với một lần bạn nhắn tin cho AI. Nếu bạn đặt tần suất quá dày (ví dụ 1 phút 1 lần), bạn sẽ tiêu tốn rất nhiều Token API. Tần suất 30-60 phút là khoảng thời gian lý tưởng nhất.

---
Tài liệu liên quan: [Tự động hóa & Cron](../../automation/cron.vi.md), [Cấu hình hệ thống](./configuration.vi.md).
