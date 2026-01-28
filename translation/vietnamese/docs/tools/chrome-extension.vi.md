---
summary: "Tiện ích Chrome: Cho phép Moltbot điều khiển các tab trình duyệt hiện có của bạn"
read_when:
  - Bạn muốn agent thao tác trực tiếp trên các tab Chrome bạn đang mở
  - Bạn cần điều khiển trình duyệt từ xa thông qua Tailscale
---
# Tiện ích Chrome (Chuyển tiếp trình duyệt)

Tiện ích mở rộng Moltbot trên Chrome cho phép agent điều khiển các **tab trình duyệt hiện có** của bạn (cửa sổ Chrome bạn đang dùng bình thường) thay vì khởi chạy một hồ sơ tách biệt hoàn toàn.

Việc kết nối hoặc ngắt kết nối được thực hiện thông qua **một nút bấm duy nhất** trên thanh công cụ của Chrome.

## Cách thức hoạt động
Có ba thành phần chính phối hợp với nhau:
1. **Dịch vụ điều khiển**: Nơi agent gửi lệnh (Gateway hoặc node host).
2. **Máy chủ chuyển tiếp cục bộ**: Cầu nối giữa Gateway và tiện ích mở rộng.
3. **Tiện ích Chrome (MV3)**: Gắn vào tab đang mở và chuyển các lệnh điều khiển từ AI tới trình duyệt.

## Khi nào nên dùng?
- Bạn đang làm việc trên một trang web và muốn AI chạy các thao tác tự động ngay trên tab đó.
- Bạn muốn AI sử dụng các phiên đăng nhập sẵn có của bạn trên trình duyệt chính mà không cần đăng nhập lại ở hồ sơ cách ly.

## Cách cài đặt
1) Chạy lệnh: `moltbot browser extension install`.
2) Lấy đường dẫn thư mục tiện ích: `moltbot browser extension path`.
3) Mở trang `chrome://extensions` trên trình duyệt:
   - Bật "Chế độ dành cho nhà phát triển" (Developer mode).
   - Nhấn "Tải tiện ích đã giải nén" (Load unpacked) và chọn thư mục ở bước 2.
4) Ghim tiện ích lên thanh công cụ.

## Cách sử dụng
- Mở tab bạn muốn AI điều khiển.
- Nhấn vào biểu tượng Moltbot trên thanh công cụ (Biểu tượng sẽ hiện chữ `ON`).
- AI bây giờ có thể thao tác trên tab này thông qua hồ sơ có tên là `chrome`.

## Lưu ý về bảo mật
**Đây là tính năng cực kỳ mạnh mẽ nhưng cũng tiềm ẩn rủi ro.**
- Khi bạn nhấn `ON`, AI có thể nhìn thấy mọi thứ trên tab đó và thực hiện các hành động (nhấn nút, nhập văn bản, chuyển trang) nhân danh bạn.
- Khi làm việc với các trang web nhạy cảm, hãy luôn giám sát hành động của AI hoặc sử dụng hồ sơ trình duyệt cô lập (`clawd`) thay thế.

---
Tài liệu liên quan: [Trình duyệt tích hợp](./browser.vi.md), [Bảo mật](../../gateway/security/index.vi.md).
