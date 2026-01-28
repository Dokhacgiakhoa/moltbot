---
summary: "Cách Moltbot chuyển đổi định danh thiết bị Apple sang tên gọi thân thiện trong ứng dụng macOS"
read_when:
  - Bạn muốn cập nhật danh sách các dòng máy iPhone/iPad/Mac mới nhất
---

# Cơ sở dữ liệu dòng máy (Tên thân thiện)

Ứng dụng macOS đi kèm hiển thị tên gọi dễ hiểu của các thiết bị Apple trong giao diện **Instances** bằng cách ánh xạ các định danh kỹ thuật (ví dụ: `iPad16,6`, `Mac16,6`) sang tên thương mại (ví dụ: iPad Pro, MacBook Pro).

## Nguồn dữ liệu

Chúng tôi sử dụng dữ liệu từ kho mã nguồn mã mở (giấy phép MIT):
- `kyle-seongwoo-jun/apple-device-identifiers`

Dữ liệu này được lưu trữ dưới dạng tệp JSON trong thư mục:
`apps/macos/Sources/Moltbot/Resources/DeviceModels/`

## Cách cập nhật danh sách mới nhất

Nếu có các dòng máy Mac hoặc iPhone mới ra mắt mà ứng dụng chưa nhận diện được tên, bạn cần:

1. Lấy mã băm (commit hash) mới nhất từ kho dữ liệu gốc ở trên.
2. Cập nhật mã băm này vào tệp `NOTICE.md` trong thư mục tài nguyên.
3. Tải các tệp JSON mới về bằng lệnh `curl`:

```bash
# Ví dụ tải danh sách cho Mac
curl -fsSL "https://raw.githubusercontent.com/.../mac-device-identifiers.json" \
  -o apps/macos/Sources/Moltbot/Resources/DeviceModels/mac-device-identifiers.json
```

4. Biên dịch lại ứng dụng macOS để áp dụng thay đổi.

---
Tài liệu liên quan: [Ứng dụng macOS](../platforms/macos.vi.md), [Thiết lập nhà phát triển](../platforms/mac/dev-setup.vi.md).
