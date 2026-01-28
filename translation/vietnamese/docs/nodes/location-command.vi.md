---
summary: "Lệnh lấy vị trí (location.get) cho các nút mạng, các chế độ cấp quyền và hành vi khi chạy ngầm"
read_when:
  - Bạn đang muốn Bot có khả năng biết vị trí GPS của các thiết bị kết nối
---

# Lệnh lấy Vị trí (Location)

## Tóm tắt
- `location.get` là một lệnh dành cho các nút mạng (thực hiện qua `node.invoke`).
- Mặc định tính năng này luôn ở trạng thái **Tắt**.
- Người dùng có thể chọn các chế độ: Tắt / Khi đang sử dụng / Luôn luôn.

## Tại sao lại có nhiều chế độ chọn?
Quyền truy cập vị trí của hệ điều hành rất phức tạp và có nhiều cấp độ:
- **iOS/macOS**: Người dùng có thể chọn giữa "Khi sử dụng ứng dụng" hoặc "Luôn luôn".
- **Android**: Truy cập vị trí khi chạy ngầm là một quyền riêng biệt, thường yêu cầu người dùng phải vào tận menu Cài đặt để bật.
- **Độ chính xác**: Người dùng có thể chọn chia sẻ vị trí chính xác (GPS) hoặc vị trí ước tính (dựa trên Wi-Fi/Sóng điện thoại).

Moltbot cung cấp giao diện để người dùng chọn chế độ mong muốn, nhưng quyền thực tế vẫn do chính hệ điều hành trên thiết bị đó quyết định.

## Mô tả lệnh: `location.get`

Dữ liệu phản hồi mẫu (JSON):
```json
{
  "lat": 10.76262, // Vĩ độ
  "lon": 106.66017, // Kinh độ
  "accuracyMeters": 10.0, // Độ chính xác (mét)
  "timestamp": "2026-01-03T12:34:56.000Z",
  "isPrecise": true // Có phải vị trí chính xác không
}
```

## Các lỗi thường gặp
- `LOCATION_DISABLED`: Chế độ chia sẻ vị trí đang tắt.
- `LOCATION_PERMISSION_REQUIRED`: Chưa được cấp quyền trên thiết bị.
- `LOCATION_TIMEOUT`: Không lấy được vị trí trong thời gian quy định.
- `LOCATION_UNAVAILABLE`: Lỗi hệ thống hoặc không có thiết bị định vị.

## Lưu ý cho người dùng
- **Tắt**: Bot không thể biết bạn ở đâu.
- **Khi đang sử dụng**: Bot chỉ lấy được vị trí khi ứng dụng Moltbot đang được mở trên màn hình.
- **Luôn luôn**: Bot có thể kiểm tra vị trí của bạn ngay cả khi điện thoại đang bỏ trong túi (nếu được hệ điều hành cho phép).
- **Vị trí chính xác**: Sử dụng GPS để lấy tọa độ chính xác. Nếu tắt, Bot chỉ biết bạn đang ở khoảng khu vực nào.

---
Tài liệu liên quan: [Các nút mạng (Nodes)](./index.vi.md), [Cài đặt trên iOS](../platforms/ios.vi.md).
