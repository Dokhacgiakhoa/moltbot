---
summary: "OAuth trong Moltbot: Trao đổi token, lưu trữ và các mô hình đa tài khoản"
read_when:
  - Bạn muốn hiểu quy trình OAuth trong Moltbot từ đầu đến cuối
  - Bạn gặp vấn đề về việc bị đăng xuất hoặc token không hợp lệ
---

# Xác thực OAuth

Moltbot hỗ trợ hình thức "xác thực đăng ký" (subscription auth) qua OAuth cho các nhà cung cấp hỗ trợ (đặc biệt là **OpenAI Codex - ChatGPT Plus**). Đối với Claude (Anthropic), vui lòng sử dụng quy trình **setup-token**.

## Nơi lưu tập trung (Token sink)

Các nhà cung cấp OAuth thường cấp một **refresh token mới** mỗi khi bạn đăng nhập hoặc làm mới token. Một số dịch vụ có tính năng: khi có token mới thì token cũ sẽ bị vô hiệu hóa ngay lập tức.

Triệu chứng thực tế:
- Bạn vừa đăng nhập Moltbot *vừa* dùng Claude Code trên cùng một tài khoản → một trong hai sẽ bị "văng" ra sau một lát.

Để hạn chế điều này, Moltbot quản lý tệp `auth-profiles.json` như một kho lưu trữ tập trung (token sink):
- Hệ thống luôn đọc thông tin đăng nhập từ **một nơi duy nhất**.
- Chúng ta có thể giữ nhiều hồ sơ tài khoản và định tuyến chúng một cách chính xác.

## Vị trí lưu trữ

Các thông tin bí mật được lưu trữ **theo từng Agent**:

- Hồ sơ xác thực (OAuth + API Keys): `~/.clawdbot/agents/<agentId>/agent/auth-profiles.json`
- Bộ nhớ đệm tự động (Runtime cache): `~/.clawdbot/agents/<agentId>/agent/auth.json` (Không nên chỉnh sửa tệp này).

## Đăng nhập qua OpenAI Codex (ChatGPT OAuth)

Quy trình hoạt động (PKCE):
1. Hệ thống tạo mã thử thách PKCE và trạng thái ngẫu nhiên.
2. Mở trình duyệt để bạn đăng nhập vào OpenAI.
3. Sau khi đăng nhập, OpenAI sẽ gửi mã về `http://127.0.0.1:1455/auth/callback`.
4. Nếu bạn đang chạy Bot trên máy chủ từ xa (không có trình duyệt), bạn có thể dán địa chỉ URL phản hồi vào Terminal để hoàn tất.
5. Hồ sơ tài khoản sẽ được lưu vào hệ thống.

Để bắt đầu, hãy dùng lệnh:
```bash
moltbot onboard
```
Và chọn phương thức `openai-codex`.

## Làm mới và Hết hạn (Refresh & Expiry)

Moltbot tự động kiểm tra thời gian hết hạn của token:
- Nếu vẫn còn hạn: Sử dụng token hiện có.
- Nếu hết hạn: Tự động thực hiện quy trình "làm mới" (refresh) và ghi đè thông tin mới vào tệp hồ sơ. Bạn gần như không bao giờ phải xử lý token thủ công.

---
Tài liệu liên quan: [Dự phòng lỗi mô hình](./model-failover.vi.md), [Lệnh Slash](../../tools/slash-commands.md).
