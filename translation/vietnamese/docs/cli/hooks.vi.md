---
summary: "Tài liệu tham khảo lệnh `moltbot hooks` (Các điểm neo tự động của Agent)"
read_when:
  - Bạn muốn quản lý các đoạn mã tự động chạy khi có sự kiện (như khởi động bot, reset chat)
---

# `moltbot hooks`

Quản lý các điểm neo (hooks) của Agent — các tác vụ tự động hóa được kích hoạt bởi các sự kiện như lệnh `/new`, `/reset`, hoặc khi Gateway khởi động.

Tài liệu liên quan:
- [Hệ thống Hooks](../../hooks.md)
- [Plugin Hooks](../../plugin.md#plugin-hooks)

## Liệt kê tất cả các Hooks

```bash
moltbot hooks list
```

Hiển thị tất cả các hooks được tìm thấy trong không gian làm việc, các thư mục được quản lý và các hooks đi kèm mặc định.

**Tùy chọn:**
- `--eligible`: Chỉ hiện các hooks đã đủ điều kiện chạy (đã đáp ứng các yêu cầu hệ thống).
- `-v, --verbose`: Hiện chi tiết lý do tại sao một hook chưa chạy được.

## Bật/Tắt một Hook

Khi bạn muốn sử dụng một tính năng tự động nào đó, bạn cần phải bật nó lên:

```bash
# Bật hook ghi nhớ phiên làm việc
moltbot hooks enable session-memory

# Tắt hook ghi nhật ký lệnh
moltbot hooks disable command-logger
```

**Lưu ý**: Sau khi bật hoặc tắt, bạn cần khởi động lại Gateway để các thay đổi có hiệu lực.

## Các Hooks đi kèm phổ biến:

### 1. session-memory
Tự động lưu lại tóm tắt nội dung cuộc trò chuyện vào thư mục "ký ức" khi bạn sử dụng lệnh `/new`. Giúp AI không bị quên những gì đã thảo luận trong các phiên trước.

### 2. command-logger
Ghi lại tất cả các lệnh đã thực hiện vào một file nhật ký tập trung để bạn có thể kiểm tra lại sau này (tại `~/.clawdbot/logs/commands.log`).

### 3. boot-md
Tự động chạy các chỉ dẫn trong file `BOOT.md` ngay khi Gateway vừa khởi động xong.

---
Tài liệu liên quan: [Kỹ năng (Skills)](./skills.vi.md), [Hệ thống Plugin](./plugins.vi.md).
