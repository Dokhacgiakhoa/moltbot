---
summary: "Các ghi chú về giao thức RPC cho trình hướng dẫn thiết lập (onboarding) và cấu trúc cấu hình"
read_when: "Khi bạn thay đổi các bước hướng dẫn thiết lập hoặc cấu trúc của các điểm cuối cấu hình"
---

# Giao thức Hướng dẫn thiết lập & Cấu hình (Thực nghiệm)

Mục đích: Chia sẻ chung giao diện hướng dẫn thiết lập (onboarding) và cấu hình trên các nền tảng CLI, ứng dụng macOS và giao diện Web.

## Các thành phần
- **Bộ máy Wizard (Hướng dẫn)**: Chia sẻ chung các phiên, lời nhắc và trạng thái thiết lập.
- **Onboarding qua CLI**: Sử dụng chung quy trình hướng dẫn như các phiên bản giao diện đồ họa.
- **Gateway RPC**: Cung cấp các điểm cuối (endpoints) cho hướng dẫn và sơ đồ cấu hình (config schema).
- **Giao diện Web**: Tự động hiển thị các biểu mẫu cấu hình dựa trên JSON Schema và các gợi ý giao diện (UI hints).

## Các lệnh Gateway RPC
- `wizard.start`: Bắt đầu quá trình hướng dẫn (chế độ cục bộ hoặc từ xa).
- `wizard.next`: Gửi câu trả lời cho bước hiện tại và nhận bước tiếp theo.
- `wizard.cancel`: Hủy bỏ quá trình hướng dẫn.
- `wizard.status`: Kiểm tra trạng thái hiện tại của quá trình thiết lập.
- `config.schema`: Lấy toàn bộ sơ đồ cấu hình của hệ thống.

## Gợi ý Giao diện (UI Hints)
- Các trường nhạy cảm (như mật khẩu, khóa API) sẽ được hiển thị dưới dạng ô nhập mật khẩu và không được ghi lại trong nhật ký.
- Nếu một phần cấu hình không được sơ đồ hỗ trợ, hệ thống sẽ tự động chuyển sang trình chỉnh sửa mã JSON thô.

---
Tài liệu liên quan: [Cấu hình Gateway](../gateway/configuration.vi.md), [Bảng điều khiển Web](../web/control-ui.vi.md).
