---
summary: "Hướng dẫn tạo các kỹ năng (skills) tùy chỉnh cho Moltbot"
read_when:
  - Bạn muốn bổ sung tính năng mới cho AI của mình
---
# Tạo kỹ năng tùy chỉnh 🛠

Moltbot được thiết kế để dễ dàng mở rộng. "Kỹ năng" (Skills) là cách chính để bổ sung năng lực mới cho trợ lý của bạn.

## Kỹ năng là gì?
Một kỹ năng thực chất là một thư mục chứa tệp `SKILL.md`. Tệp này cung cấp hướng dẫn và định nghĩa công cụ cho mô hình ngôn ngữ (LLM). Kỹ năng cũng có thể bao gồm các kịch bản (scripts) hoặc tài liệu hỗ trợ.

## Từng bước tạo kỹ năng đầu tiên

### 1. Tạo thư mục
Kỹ năng nên nằm trong không gian làm việc của bạn, thường là ở thư mục `skills/`.
```bash
mkdir -p skills/xin-chao
```

### 2. Định nghĩa tệp `SKILL.md`
Tạo tệp `SKILL.md` bên trong thư mục đó. Tệp này sử dụng cấu trúc YAML ở đầu để khai báo thông tin và Markdown cho phần hướng dẫn.

```markdown
---
name: xin_chao
description: Một kỹ năng đơn giản để AI biết chào hỏi.
---

# Kỹ năng Xin Chào
Khi người dùng yêu cầu lời chào, hãy sử dụng công cụ `echo` để trả lời: "Xin chào từ kỹ năng tùy chỉnh của bạn!".
```

### 3. Thêm công cụ (Tùy chọn)
Bạn có thể định nghĩa các công cụ mới hoặc hướng dẫn AI sử dụng các công cụ hệ thống sẵn có (như `bash` hoặc `browser`).

### 4. Làm mới Moltbot
Yêu cầu AI "làm mới kỹ năng" (refresh skills) hoặc khởi động lại Gateway. Moltbot sẽ tự động tìm thấy thư mục mới và nạp dữ liệu từ `SKILL.md`.

## Quy tắc vàng
- **Ngắn gọn**: Hãy hướng dẫn AI *cần làm gì*, đừng dạy nó cách để trở thành một AI.
- **An toàn là trên hết**: Nếu kỹ năng của bạn sử dụng lệnh `bash`, hãy đảm bảo các chỉ dẫn không để lộ lỗ hổng cho phép người dùng lạ chạy lệnh hệ thống trái phép.
- **Kiểm tra kỹ**: Dùng lệnh `moltbot agent --message "thử kỹ năng mới"` để kiểm tra trực tiếp.

---
Tài liệu liên quan: [ClawdHub](./clawdhub.vi.md), [Cấu hình kỹ năng](./skills-config.vi.md).
