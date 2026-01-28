---
title: Lệnh Sandbox (Môi trường cô lập)
summary: "Quản lý các container sandbox và kiểm tra các chính sách bảo mật thực tế"
read_when: "Bạn đang quản lý các container Docker hoặc gỡ lỗi về phân quyền của Agent"
---

# Lệnh Sandbox

Quản lý các container dựa trên Docker để thực thi các lệnh của Agent trong môi trường cô lập, đảm bảo an toàn cho hệ thống chủ.

Tài liệu liên quan:
- Bảo mật: [Cơ chế Sandboxing](../gateway/sandboxing.vi.md)

## Các lệnh chính

### 1. `moltbot sandbox explain`
Giải thích chi tiết về chế độ sandbox đang hoạt động, phạm vi truy cập của Agent vào các thư mục và các công cụ được cấp quyền. Rất hữu ích khi bạn cần biết tại sao một lệnh bị bot từ chối thực hiện.
```bash
moltbot sandbox explain
```

### 2. `moltbot sandbox list`
Liệt kê tất cả các container sandbox đang chạy kèm theo trạng thái và cấu hình của chúng.
```bash
moltbot sandbox list
```

### 3. `moltbot sandbox recreate`
Buộc xóa và tạo lại các container sandbox. Lệnh này thường dùng sau khi bạn cập nhật bản image Docker mới hoặc thay đổi cấu hình bảo mật.
```bash
# Tạo lại tất cả các container
moltbot sandbox recreate --all

# Chỉ tạo lại container cho một Agent cụ thể
moltbot sandbox recreate --agent mybot
```

## Tại sao cần lệnh này?
Containers thường chỉ bị xóa sau 24 giờ không hoạt động. Nếu bạn vừa thay đổi cấu hình hoặc cập nhật Moltbot, các container cũ có thể vẫn đang chạy với cài đặt lỗi thời. Lệnh `recreate` đảm bảo mọi thứ được làm mới theo cấu hình mới nhất của bạn.

---
Tài liệu liên quan: [Cấu hình Gateway](../gateway/configuration.vi.md), [Hướng dẫn cài đặt Docker](../../install/docker.md).
