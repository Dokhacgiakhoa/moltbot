---
summary: "Hỗ trợ tài khoản Zalo cá nhân qua zca-cli (đăng nhập QR), khả năng và cấu hình"
read_when:
  - Thiết lập Zalo Cá nhân cho Moltbot
  - Kiểm tra luồng đăng nhập hoặc gửi tin nhắn Zalo Cá nhân
---
# Zalo Cá nhân (phiên bản không chính thức)

Trạng thái: Đang thử nghiệm (experimental). Bản tích hợp này tự động hóa một **tài khoản Zalo cá nhân** thông qua công cụ `zca-cli`.

> **Cảnh báo:** Đây là bản tích hợp không chính thức và có thể dẫn đến việc tài khoản bị khóa/cấm. Hãy tự chịu rủi ro khi sử dụng.

## Yêu cầu Plugin
Zalo Cá nhân được cung cấp dưới dạng plugin và không đi kèm sẵn trong bản cài đặt cốt lõi.
- Cài đặt qua CLI: `moltbot plugins install @moltbot/zalouser`
- Chi tiết: [Plugins](../plugin.vi.md)

## Điều kiện tiên quyết: zca-cli
Máy chạy Gateway phải cài đặt sẵn binary chất `zca` trong `PATH`.

- Kiểm tra: `zca --version`
- Nếu thiếu, hãy cài đặt zca-cli theo tài liệu hướng dẫn của họ.

## Thiết lập nhanh (Dành cho người mới)
1) Cài đặt plugin (xem ở trên).
2) Đăng nhập (Quét QR, ngay trên máy chạy Gateway):
   - `moltbot channels login --channel zalouser`
   - Quét mã QR trong terminal bằng ứng dụng Zalo trên điện thoại.
3) Bật kênh trong cấu hình:

```json5
{
  channels: {
    zalouser: {
      enabled: true,
      dmPolicy: "pairing"
    }
  }
}
```

4) Khởi động lại Gateway.
5) Quyền truy cập DM mặc định là `pairing` (ghép đôi); phê duyệt mã ghép đôi trong lần liên lạc đầu tiên.

## Tổng quan
- Sử dụng `zca listen` để nhận tin nhắn đến.
- Sử dụng `zca msg ...` để gửi phản hồi (văn bản/media/liên kết).
- Thiết kế cho các trường hợp sử dụng "tài khoản cá nhân" khi không thể dùng Zalo Bot API.

## Đặt tên
ID của kênh là `zalouser` để phân biệt rõ ràng đây là việc tự động hóa một **tài khoản người dùng Zalo cá nhân** (không chính thức). Chúng tôi giữ ID `zalo` cho các tích hợp Zalo API chính thức trong tương lai.

## Kiểm soát quyền truy cập
- DM: `channels.zalouser.dmPolicy` hỗ trợ: `pairing | allowlist | open | disabled` (mặc định: `pairing`).
- Nhóm: `channels.zalouser.groupPolicy` hỗ trợ: `open | allowlist | disabled`.
- Bạn có thể dùng tên nhóm hoặc ID nhóm trong danh sách phê duyệt `allowlist`.

---
Tài liệu liên quan: [Bảo mật](../gateway/security.vi.md), [Plugins](../plugin.vi.md).
