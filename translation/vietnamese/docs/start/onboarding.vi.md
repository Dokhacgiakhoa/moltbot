---
summary: "Quy trình thiết lập ban đầu (onboarding) cho ứng dụng Moltbot trên macOS"
read_when:
  - Thiết kế trợ lý thiết lập trên macOS
  - Triển khai thiết lập xác thực hoặc danh tính
---
# Thiết lập ban đầu (Ứng dụng macOS)

Tài liệu này mô tả quy trình thiết lập ban đầu hiện tại cho lần chạy đầu tiên. Mục tiêu là tạo ra trải nghiệm "ngày 0" mượt mà: chọn nơi chạy Gateway, kết nối xác thực, chạy trình hướng dẫn (wizard) và để agent tự khởi tạo không gian làm việc.

## Thứ tự các trang (hiện tại)

1) Chào mừng + Thông báo bảo mật
2) **Lựa chọn Gateway** (Cục bộ / Từ xa / Cấu hình sau)
3) **Xác thực (Anthropic OAuth)** — chỉ dành cho bản cục bộ (local)
4) **Trình hướng dẫn thiết lập (Wizard)** (Điều khiển bởi Gateway)
5) **Quyền truy cập** (Yêu cầu TCC)
6) **CLI** (Tùy chọn)
7) **Chat thiết lập** (Phiên làm việc dành riêng)
8) Sẵn sàng

## 1) Cục bộ (Local) so với Từ xa (Remote)

**Gateway** sẽ chạy ở đâu?

- **Local (trên máy Mac này):** quy trình thiết lập có thể chạy các luồng OAuth và ghi thông tin đăng nhập ngay tại máy.
- **Remote (qua SSH/Tailnet):** quy trình thiết lập **không** chạy OAuth cục bộ; thông tin đăng nhập phải có sẵn trên máy chủ gateway.
- **Cấu hình sau:** bỏ qua thiết lập và để ứng dụng ở trạng thái chưa cấu hình.

Mẹo về xác thực Gateway:
- Wizard hiện tạo một **token** kể cả trên loopback, vì vậy các client WS cục bộ phải xác thực.
- Nếu bạn tắt xác thực, bất kỳ tiến trình cục bộ nào cũng có thể kết nối; chỉ sử dụng điều này trên các máy hoàn toàn tin cậy.

## 2) Xác thực chỉ dành cho Local (Anthropic OAuth)

Ứng dụng macOS hỗ trợ Anthropic OAuth (Claude Pro/Max). Quy trình:

- Mở trình duyệt để thực hiện OAuth (PKCE)
- Yêu cầu người dùng dán giá trị `code#state`
- Ghi thông tin đăng nhập vào `~/.clawdbot/credentials/oauth.json`

Các nhà cung cấp khác (OpenAI, API tùy chỉnh) hiện được cấu hình qua biến môi trường hoặc các file cấu hình.

## 3) Trình hướng dẫn thiết lập (Wizard)

Ứng dụng có thể chạy cùng một trình hướng dẫn thiết lập như CLI. Điều này giúp đồng bộ hành vi giữa ứng dụng và Gateway, đồng thời tránh việc trùng lặp logic trong SwiftUI.

## 4) Quyền truy cập

Quy trình thiết lập yêu cầu các quyền TCC cần thiết cho:

- Thông báo (Notifications)
- Quyền truy cập (Accessibility)
- Ghi màn hình (Screen Recording)
- Microphone / Nhận dạng giọng nói (Microphone / Speech Recognition)
- Tự động hóa (AppleScript)

## 5) CLI (Tùy chọn)

Ứng dụng có thể cài đặt CLI `moltbot` global thông qua npm/pnpm để các quy trình trong terminal và các tác vụ launchd có thể hoạt động ngay lập tức.

## 6) Chat thiết lập (Onboarding chat)

Sau khi thiết lập, ứng dụng mở một phiên chat thiết lập dành riêng để agent có thể tự giới thiệu và hướng dẫn các bước tiếp theo. Điều này giúp tách biệt các hướng dẫn lần đầu chạy khỏi các cuộc hội thoại bình thường của bạn.

## Nghi thức Khởi tạo Agent (Agent bootstrap)

Trong lần chạy agent đầu tiên, Moltbot sẽ khởi tạo một không gian làm việc (workspace - mặc định là `~/clawd`):

- Tạo các file `AGENTS.md`, `BOOTSTRAP.md`, `IDENTITY.md`, `USER.md`.
- Chạy một nghi thức Q&A ngắn (từng câu hỏi một).
- Ghi danh tính + sở thích vào `IDENTITY.md`, `USER.md`, `SOUL.md`.
- Xóa file `BOOTSTRAP.md` sau khi hoàn thành để nghi thức này chỉ chạy một lần duy nhất.

## Ghi chú về chế độ Remote

Khi Gateway chạy trên một máy khác, các file thông tin đăng nhập và không gian làm việc sẽ nằm **trên máy chủ đó**. Nếu bạn cần dùng OAuth ở chế độ remote, hãy tạo các file sau trên máy chủ gateway:

- `~/.clawdbot/credentials/oauth.json`
- `~/.clawdbot/agents/<agentId>/agent/auth-profiles.json`
