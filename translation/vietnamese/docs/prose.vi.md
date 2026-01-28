---
summary: "OpenProse: Quy trình làm việc .prose, lệnh điều khiển và trạng thái trong Moltbot"
---

# OpenProse

OpenProse là một định dạng quy trình làm việc (workflow) dựa trên Markdown, được thiết kế để điều phối các phiên làm việc của AI. Trong Moltbot, nó được cung cấp dưới dạng một plugin bao gồm bộ kỹ năng OpenProse và lệnh điều khiển `/prose`. Các chương trình được viết trong tệp `.prose` và có thể khởi tạo nhiều Agent phụ với quy trình điều khiển rõ ràng.

Trang chủ chính thức: https://www.prose.md

## Khả năng của OpenProse

- Nghiên cứu và tổng hợp thông tin đa Agent với khả năng chạy song song.
- Quy trình làm việc có thể lặp lại và an toàn (như đánh giá mã nguồn, phân loại sự cố, quy trình tạo nội dung).
- Các chương trình `.prose` có thể tái sử dụng trên nhiều môi trường chạy Agent khác nhau.

## Cài đặt và Kích hoạt

Plugin OpenProse mặc định bị tắt. Bạn có thể bật nó bằng lệnh:

```bash
moltbot plugins enable open-prose
```

Sau khi bật, hãy khởi động lại Gateway.

## Các lệnh điều khiển (Slash commands)

OpenProse đăng ký lệnh `/prose` để người dùng gọi các kỹ năng. Một số lệnh phổ biến:

- `/prose help`: Xem hướng dẫn.
- `/prose run <tên_tệp.prose>`: Chạy một tệp quy trình làm việc cục bộ.
- `/prose run <URL>`: Chạy tệp quy trình từ một địa chỉ web.
- `/prose examples`: Xem các ví dụ mẫu.

## Ví dụ: Một tệp `.prose` đơn giản

```prose
# Nghiên cứu và tóm tắt với hai Agent chạy song song.

input topic: "Chủ đề nghiên cứu là gì?"

agent researcher:
  model: sonnet
  prompt: "Bạn là chuyên gia nghiên cứu sâu và trích dẫn nguồn đầy đủ."

agent writer:
  model: opus
  prompt: "Bạn là người viết tóm tắt súc tích."

parallel:
  findings = session: researcher
    prompt: "Nghiên cứu về {topic}."
  draft = session: writer
    prompt: "Tóm tắt về {topic}."

session "Kết hợp kết quả nghiên cứu và bản thảo thành câu trả lời cuối cùng."
context: { findings, draft }
```

## Vị trí lưu trữ dữ liệu

OpenProse lưu trạng thái tại thư mục `.prose/` trong không gian làm việc của bạn. Thư mục này chứa nhật ký các lần chạy (`runs`), thông tin các Agent phụ và các tệp cấu hình môi trường.

## Lưu ý về an toàn

Hãy coi các tệp `.prose` như mã nguồn chương trình. Hãy kiểm tra kỹ nội dung trước khi chạy. Sử dụng danh sách cho phép (allowlist) của Moltbot để kiểm soát các tác động ngoài ý muốn của Agent.

---
Tài liệu liên quan: [Plugin](../plugin.vi.md), [Kỹ năng](../tools/skills.vi.md), [Cấu hình kỹ năng](../tools/skills-config.vi.md).
