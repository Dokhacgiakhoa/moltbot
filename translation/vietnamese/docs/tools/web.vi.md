---
summary: "Các công cụ tìm kiếm và tải nội dung web (Brave Search, Perplexity)"
read_when:
  - Bạn muốn cho phép AI truy cập internet để tìm thông tin trực tuyến
---
# Công cụ Web

Moltbot cung cấp hai công cụ web nhẹ nhàng:

- `web_search`: Tìm kiếm web thông qua Brave Search (mặc định) hoặc Perplexity Sonar.
- `web_fetch`: Tải nội dung từ một địa chỉ URL và chuyển đổi HTML sang định dạng Markdown hoặc văn bản dễ đọc.

**Lưu ý**: Đây là các công cụ tải dữ liệu tĩnh. Đối với các trang web yêu cầu đăng nhập hoặc có nhiều hiệu ứng chuyển động (JavaScript), hãy sử dụng [Công cụ Trình duyệt](./browser.vi.md).

## Cách thức hoạt động
- **Tìm kiếm**: AI sẽ gửi từ khóa tới nhà cung cấp (Brave hoặc Perplexity) và nhận về các kết quả kèm theo tóm tắt nội dung.
- **Tải nội dung**: AI sẽ lấy nội dung văn bản chính của trang web, loại bỏ các quảng cáo và menu thừa để dễ dàng phân tích và tiết kiệm chi phí token. Các kết quả này được lưu tạm trong bộ nhớ đệm (cache) trong 15 phút.

## Lựa chọn nhà cung cấp tìm kiếm
- **Brave Search** (Mặc định): Nhanh, kết quả có cấu trúc rõ ràng (tiêu đề, URL, đoạn trích).
- **Perplexity**: Cung cấp các câu trả lời do AI tổng hợp kèm theo trích dẫn nguồn từ kết quả tìm kiếm theo thời gian thực.

## Cài đặt mã API (API Key)
Để sử dụng các tính năng này, bạn cần cung cấp mã API tương ứng (Brave hoặc OpenRouter/Perplexity). Bạn có thể thiết lập nhanh qua lệnh:
```bash
moltbot configure --section web
```
Hoặc cấu hình trực tiếp trong tệp `moltbot.json`.

## Các tính năng nâng cao
Bạn có thể yêu cầu AI tìm kiếm theo quốc gia cụ thể (ví dụ: `country: "VN"`) hoặc độ tươi mới của thông tin (ví dụ: trong vòng 1 tuần qua).

---
Tài liệu liên quan: [Firecrawl (Trích xuất nâng cao)](./firecrawl.vi.md), [Điều khiển trình duyệt](./browser.vi.md).
