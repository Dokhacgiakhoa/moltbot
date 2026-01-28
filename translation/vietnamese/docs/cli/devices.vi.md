---
summary: "Tài liệu tham khảo lệnh `moltbot devices` (Ghép nối thiết bị + Thu hồi/Làm mới Token)"
read_when:
  - Bạn muốn phê duyệt các yêu cầu ghép nối thiết bị mới
  - Bạn cần làm mới hoặc hủy bỏ mã Token của một thiết bị cụ thể
---

# `moltbot devices`

Quản lý các yêu cầu ghép nối thiết bị và các mã Token (mã định danh bảo mật) được cấp riêng cho từng thiết bị.

## Các lệnh chính

### 1. `moltbot devices list`
Liệt kê các yêu cầu đang chờ và các thiết bị đã ghép nối thành công.
```bash
moltbot devices list
```

### 2. `moltbot devices approve <ID_yeu_cau>`
Phê duyệt một thiết bị mới được phép kết nối vào hệ thống của bạn.
```bash
moltbot devices approve req_abc123
```

### 3. Làm mới hoặc Hủy bỏ Token
Nhằm đảm bảo an toàn, bạn có thể thay đổi hoặc thu hồi quyền truy cập của bất kỳ thiết bị nào:
```bash
# Làm mới token cho thiết bị
moltbot devices rotate --device <ID_thiet_bi> --role operator

# Hủy bỏ quyền truy cập của thiết bị
moltbot devices revoke --device <ID_thiet_bi> --role node
```

## Lưu ý về bảo mật
- Khi bạn làm mới (rotate) token, hệ thống sẽ trả về một mã token mới. Hãy giữ nó thật cẩn thận và không chia sẻ cho người khác.
- Chỉ những người có quyền quản trị (`admin`) mới có thể thực hiện các lệnh này.

---
Tài liệu liên quan: [Cơ chế Ghép nối Gateway](../gateway/pairing.vi.md), [Bảo mật Gateway](../gateway/security/index.vi.md).
