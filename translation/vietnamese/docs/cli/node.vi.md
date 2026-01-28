---
summary: "Tài liệu tham khảo lệnh `moltbot node` (Chạy host node không giao diện)"
read_when:
  - Bạn muốn chạy Moltbot trên các máy tính khác trong mạng nội bộ để thực hiện lệnh từ xa
---

# `moltbot node`

Khởi chạy một **máy chủ node (headless node host)** giúp kết nối với Gateway và cho phép thực thi các lệnh hệ thống (`system.run`) trên chính máy tính đó.

## Tại sao nên dùng Node Host?
Sử dụng node host khi bạn muốn Agent có thể **chạy lệnh trên các máy tính khác** trong mạng của bạn mà không cần phải cài đặt đầy đủ ứng dụng Moltbot trên đó.

Ví dụ: 
- Chạy lệnh trên máy chủ Linux/Windows từ xa.
- Giữ cho tiến trình chính được bảo vệ trong sandbox trên Gateway, nhưng ủy quyền thực hiện các lệnh đã được phê duyệt trên các máy chủ cụ thể.

## Khởi chạy trực tiếp (Foreground)
```bash
moltbot node run --host <dia-chi-gateway> --port 18789
```

## Cài đặt như một dịch vụ chạy ngầm
```bash
moltbot node install --host <dia-chi-gateway> --port 18789

# Quản lý dịch vụ
moltbot node status
moltbot node restart
moltbot node stop
```

## Quy trình ghép nối (Pairing)
Lần đầu tiên kết nối, node host sẽ gửi một yêu cầu ghép nối tới Gateway. Bạn cần phê duyệt yêu cầu này trên máy tính chạy Gateway bằng lệnh:
```bash
moltbot nodes pending
moltbot nodes approve <ID_yeu_cau>
```

---
Tài liệu liên quan: [Thành phần Node](../../nodes.vi.md), [Phê duyệt lệnh](../../tools/exec-approvals.md).
