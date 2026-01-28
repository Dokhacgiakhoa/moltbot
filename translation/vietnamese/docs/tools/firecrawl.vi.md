---
summary: "Sử dụng Firecrawl làm bộ trích xuất dữ liệu web dự phòng (chống bot và dùng bộ nhớ đệm)"
read_when:
  - Bạn muốn sử dụng Firecrawl để đọc nội dung các trang web khó (nhiều JS)
  - Cần vượt qua các rào cản chống trích xuất dữ liệu của các trang web lớn
---
# Firecrawl

Moltbot có thể sử dụng **Firecrawl** như một giải pháp dự phòng cho công cụ `web_fetch`. Đây là một dịch vụ lưu trữ trích xuất nội dung web mạnh mẽ, hỗ trợ vượt qua các cơ chế chống bot và hỗ trợ lưu dữ liệu vào bộ nhớ đệm (cache). Điều này cực kỳ hữu ích cho các trang web sử dụng nhiều JavaScript hoặc các trang thường xuyên chặn các lượt truy cập HTTP thông thường.

## Cách thiết lập
1) Tạo tài khoản Firecrawl và lấy **API Key**.
2) Lưu mã này vào cấu hình Moltbot hoặc cài đặt biến môi trường `FIRECRAWL_API_KEY`.

## Tại sao nên dùng Firecrawl?
- **Chế độ ẩn danh (Stealth)**: Firecrawl tự động sử dụng các máy chủ ủy quyền (proxies) thông minh để tránh bị các trang web phát hiện là bot.
- **Trích xuất nội dung sạch**: Thay vì lấy toàn bộ mã nguồn HTML rối rắm, Firecrawl có thể chỉ lấy nội dung văn bản chính, giúp AI dễ hiểu hơn và tiết kiệm chi phí token.
- **Tốc độ**: Với cơ chế bộ nhớ đệm, các trang web bạn đã truy cập gần đây sẽ được tải lại ngay lập tức mà không cần trích xuất lại từ đầu.

## Cách Moltbot ưu tiên xử lý web
Khi bạn yêu cầu AI đọc một trang web, Moltbot sẽ thử theo thứ tự:
1. Tự đọc bằng thư viện nội bộ (nhanh và miễn phí).
2. Dùng Firecrawl (nếu bạn đã cài đặt).
3. Dọn dẹp HTML cơ bản (phương án cuối cùng).

---
Tài liệu liên quan: [Công cụ Web](./web.vi.md), [Điều khiển trình duyệt](./browser.vi.md).
