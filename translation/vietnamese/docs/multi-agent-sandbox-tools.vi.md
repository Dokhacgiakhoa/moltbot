---
summary: "Quy tắc thiết lập Hộp cát (Sandbox) và giới hạn công cụ cho từng Agent"
---
# Cấu hình Hộp cát & Công cụ Đa Agent

## Tổng quan

Trong chế độ đa Agent, mỗi Agent có thể có các thiết lập riêng biệt về:
- **Cấu hình Hộp cát (Sandbox)**: Kiểm soát mức độ an toàn và cách ly khi thực thi mã nguồn.
- **Giới hạn công cụ (Tool restrictions)**: Cho phép hoặc từ chối sử dụng các công cụ cụ thể (như đọc/ghi file, truy cập trình duyệt).

Điều này giúp bạn vận hành nhiều Agent với các mức độ bảo mật khác nhau:
- **Trợ lý cá nhân**: Toàn quyền truy cập.
- **Agent cho gia đình/đồng nghiệp**: Giới hạn các công cụ nhạy cảm.
- **Agent công khai**: Luôn chạy trong Hộp cát (Docker) để đảm bảo an toàn tuyệt đối.

## Ví dụ cấu hình

### Ví dụ 1: Agent cá nhân (toàn quyền) + Agent gia đình (giới hạn)

```json
{
  "agents": {
    "list": [
      {
        "id": "main",
        "name": "Trợ lý cá nhân",
        "sandbox": { "mode": "off" }
      },
      {
        "id": "family",
        "name": "Bot gia đình",
        "sandbox": {
          "mode": "all",
          "scope": "agent"
        },
        "tools": {
          "allow": ["read"],
          "deny": ["exec", "write", "edit", "browser"]
        }
      }
    ]
  }
}
```

## Thứ tự ưu tiên của Cấu hình

Khi có cả cấu hình chung và cấu hình riêng cho từng Agent:
- Cấu hình riêng của Agent luôn **ghi đè** cấu hình chung.
- Đối với công cụ: Mỗi cấp độ (Chung → Agent → Hộp cát) có thể thắt chặt thêm các hạn chế, nhưng **không thể cấp lại quyền** cho một công cụ đã bị từ chối ở cấp độ trước đó.

## Các nhóm công cụ (Viết tắt)

Bạn có thể sử dụng các nhóm để cấp quyền nhanh:
- `group:runtime`: Các lệnh thực thi hệ thống (`exec`, `bash`).
- `group:fs`: Các lệnh về tệp tin (`read`, `write`, `edit`).
- `group:ui`: Trình duyệt và canvas.
- `group:messaging`: Gửi tin nhắn.
- `group:moltbot`: Tất cả các công cụ mặc định của Moltbot.

## Chế độ Nâng cao (Elevated Mode)

Đây là chế độ cho phép Agent thực thi các lệnh nhạy cảm dựa trên danh sách người gửi được tin tưởng. Bạn có thể tắt chế độ này cho các Agent không tin cậy để tăng tính bảo mật.

## Lưu ý về chế độ "non-main"

Mặc định, các cuộc hội thoại trong nhóm hoặc các kênh không phải chính (main) sẽ bị coi là `non-main` và tự động bị đẩy vào Hộp cát. Nếu bạn muốn một Agent cụ thể không bao giờ bị Hộp cát hóa, hãy đặt `sandbox.mode: "off"`.

---
Tài liệu liên quan: [Điều hướng đa Agent](../concepts/multi-agent.vi.md), [Thiết lập Hộp cát](../gateway/sandboxing.vi.md).
