---
summary: "Trung tâm xử lý sự cố: Triệu chứng → Kiểm tra → Cách sửa"
read_when:
  - Bạn thấy một thông báo lỗi và muốn tìm cách khắc phục
  - Bộ cài báo "thành công" nhưng lệnh CLI không hoạt động
---

# Xử lý sự cố (Troubleshooting)

## 60 giây đầu tiên

Hãy chạy các lệnh này theo thứ tự:

```bash
moltbot status
moltbot status --all
moltbot gateway probe
moltbot logs --follow
moltbot doctor
```

Nếu Gateway có thể kết nối được, hãy kiểm tra sâu hơn bằng lệnh:

```bash
moltbot status --deep
```

## Các trường hợp lỗi phổ biến

### Lỗi `moltbot: command not found`

Hầu hết là do vấn đề về đường dẫn (PATH) của Node/npm. Hãy bắt đầu từ đây:
- [Kiểm tra PATH của Node/npm](../../install.vi.md#nodejs--npm-path-sanity)

### Bộ cài bị lỗi (hoặc bạn muốn xem nhật ký đầy đủ)

Hãy chạy lại bộ cài ở chế độ chi tiết (verbose) để xem toàn bộ quá trình:

```bash
curl -fsSL https://molt.bot/install.sh | bash -s -- --verbose
```

### Gateway báo "Unauthorized", không thể kết nối hoặc liên tục kết nối lại

- [Xử lý sự cố Gateway](../../gateway/troubleshooting.vi.md)
- [Xác thực Gateway](../../gateway/authentication.vi.md)

### Giao diện điều khiển (Control UI) lỗi trên HTTP (yêu cầu nhận diện thiết bị)

- [Xử lý sự cố Gateway](../../gateway/troubleshooting.vi.md)
- [Giao diện điều khiển](../../web/control-ui.vi.md#insecure-http)

### Lỗi SSL khi truy cập `docs.molt.bot` (Do mạng Comcast/Xfinity)

Một số nhà mạng có thể chặn tên miền này. Hãy thử tắt "Advanced Security" hoặc sử dụng VPN/Hotspot điện thoại để kiểm tra.

### Dịch vụ báo đang chạy nhưng lệnh kiểm tra (probe) thất bại

- [Xử lý sự cố Gateway](../../gateway/troubleshooting.vi.md)
- [Tiến trình chạy ngầm / Dịch vụ](../../gateway/background-process.vi.md)

### Lỗi Mô hình/Xác thực (Hết hạn mức, lỗi thanh toán)

- [Mô hình AI](../../cli/models.vi.md)
- [Khái niệm Xác thực / OAuth](../../concepts/oauth.vi.md)

### Khi bạn muốn gửi yêu cầu hỗ trợ

Hãy đính kèm báo cáo an toàn từ lệnh sau:

```bash
moltbot status --all
```

Đồng thời, nếu có thể, hãy gửi kèm vài dòng cuối của nhật ký từ lệnh `moltbot logs --follow`.

---
Tài liệu liên quan: [Cài đặt](../../install.vi.md), [Xác thực Gateway](../../gateway/authentication.vi.md).
