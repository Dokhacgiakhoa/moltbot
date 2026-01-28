---
summary: "Phát đi tin nhắn WhatsApp cho nhiều Agent cùng lúc"
status: experimental
---

# Nhóm phát tin nhắn (Broadcast Groups)

**Trạng thái:** Thực nghiệm (Experimental)  
**Phiên bản:** Bổ sung từ 2026.1.9

## Tổng quan

Nhóm phát tin nhắn (Broadcast Groups) cho phép nhiều Agent cùng lúc xử lý và phản hồi cho một tin nhắn duy nhất. Điều này giúp bạn tạo ra các nhóm Agent chuyên biệt làm việc cùng nhau trong một nhóm WhatsApp hoặc chat riêng — tất cả chỉ dùng một số điện thoại duy nhất.

Phạm vi hiện tại: **Chỉ dành cho WhatsApp**.

## Các trường hợp sử dụng

### 1. Nhóm Agent chuyên biệt
Triển khai nhiều Agent với các trách nhiệm riêng biệt:
- **CodeReviewer**: Đánh giá mã nguồn.
- **DocumentationBot**: Tạo tài liệu hướng dẫn.
- **SecurityAuditor**: Kiểm tra lỗ hổng bảo mật.

Tất cả các Agent này cùng nhận một tin nhắn và đưa ra góc nhìn chuyên môn của họ.

### 2. Hỗ trợ đa ngôn ngữ
Nhiều Agent phản hồi bằng các ngôn ngữ khác nhau (Anh, Đức, Tây Ban Nha) cho cùng một câu hỏi của khách hàng.

## Cấu hình

Thêm mục `broadcast` vào cấu hình chính. Các khóa (keys) là ID của đối tượng WhatsApp (JID nhóm hoặc số điện thoại).

```json
{
  "broadcast": {
    "120363403215116621@g.us": ["alfred", "baerbel", "assistant3"]
  }
}
```

**Kết quả:** Khi có tin nhắn trong nhóm này, Moltbot sẽ gọi cả ba Agent cùng lúc.

### Chiến lược xử lý (`strategy`)

- **parallel** (Mặc định): Tất cả các Agent xử lý đồng thời.
- **sequential**: Các Agent xử lý lần lượt theo thứ tự (Agent sau đợi Agent trước hoàn thành).

## Cách hoạt động

1. **Tin nhắn đến**: Hệ thống kiểm tra xem ID nhóm/người gửi có nằm trong danh sách `broadcast` không.
2. **Nếu có**:
   - Tất cả Agent trong danh sách sẽ xử lý tin nhắn.
   - Mỗi Agent có một **phiên làm việc (session) riêng biệt** và bối cảnh cách ly.
   - Các Agent không nhìn thấy tin nhắn của nhau (theo thiết kế).
3. **Nếu không có**: Áp dụng quy tắc điều hướng tin nhắn thông thường.

## Lưu ý quan trọng

- **Cách ly phiên**: Các Agent hoàn toàn độc lập về lịch sử trò chuyện, không gian làm việc và quyền hạn công cụ.
- **Giới hạn tự nhiên**: Không có giới hạn cứng về số lượng Agent, nhưng dùng quá 10 Agent cùng lúc có thể làm chậm hệ thống.
- **Thứ tự tin nhắn**: Trong chế độ song song (`parallel`), thứ tự tin nhắn phản hồi trên WhatsApp có thể không cố định.

---
Tài liệu liên quan: [Cấu hình đa Agent](../multi-agent-sandbox-tools.vi.md), [Quản lý phiên](../concepts/session.vi.md).
