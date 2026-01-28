---
summary: "Hướng dẫn thiết lập: giữ cho cấu hình Moltbot của bạn mang tính cá nhân trong khi vẫn luôn cập nhật"
read_when:
  - Thiết lập trên một máy mới
  - Muốn dùng bản "mới nhất & xịn nhất" mà không làm hỏng cấu hình cá nhân
---

# Thiết lập (Setup)

Cập nhật lần cuối: 01/01/2026

## Tóm tắt (TL;DR)
- **Cấu hình cá nhân nằm ngoài repo:** `~/clawd` (workspace) + `~/.clawdbot/moltbot.json` (config).
- **Quy trình ổn định (Stable):** cài đặt ứng dụng macOS; để nó tự chạy Gateway đi kèm.
- **Quy trình cho Dev (Bleeding edge):** tự chạy Gateway qua lệnh `pnpm gateway:watch`, sau đó để ứng dụng macOS kết nối ở chế độ Local.

## Điều kiện tiên quyết (Cài từ nguồn)
- Node `>=22`
- `pnpm`
- Docker (tùy chọn; chỉ dùng cho thiết lập container/e2e — xem [Docker](../install/docker.vi.md))

## Chiến lược cá nhân hóa (Để cập nhật không gây đau khổ)

Nếu bạn muốn "100% theo ý mình" *mà vẫn* cập nhật dễ dàng, hãy giữ các tùy chỉnh của bạn trong:

- **Cấu hình (Config):** `~/.clawdbot/moltbot.json` (định dạng JSON/JSON5)
- **Không gian làm việc (Workspace):** `~/clawd` (kỹ năng, câu lệnh prompts, ký ức; nên biến nó thành một kho git riêng tư)

Khởi tạo lần đầu:

```bash
moltbot setup
```

Từ bên trong repo này, sử dụng lối vào CLI cục bộ:

```bash
moltbot setup
```

Nếu bạn chưa cài bản global, hãy chạy qua lệnh `pnpm moltbot setup`.

## Quy trình ổn định (Ưu tiên ứng dụng macOS)

1) Cài đặt + khởi chạy **Moltbot.app** (trên thanh menu).
2) Hoàn thành danh sách kiểm tra thiết lập/quyền (cấp quyền TCC).
3) Đảm bảo Gateway ở chế độ **Local** và đang chạy (ứng dụng sẽ tự quản lý nó).
4) Liên kết các giao diện (ví dụ: WhatsApp):

```bash
moltbot channels login
```

5) Kiểm tra nhanh:

```bash
moltbot health
```

Nếu tính năng onboarding không có sẵn trong bản build của bạn:
- Chạy `moltbot setup`, sau đó là `moltbot channels login`, rồi bắt đầu Gateway thủ công (`moltbot gateway`).

## Quy trình cho Dev (Chạy Gateway trong terminal)

Mục tiêu: chỉnh sửa Gateway bằng TypeScript, có tính năng tự nạp lại (hot reload) mà vẫn giữ giao diện ứng dụng macOS kết nối.

### 0) (Tùy chọn) Chạy ứng dụng macOS từ mã nguồn

Nếu bạn cũng muốn chạy app macOS bản mới nhất:

```bash
./scripts/restart-mac.sh
```

### 1) Bắt đầu Gateway bản dev

```bash
pnpm install
pnpm gateway:watch
```

`gateway:watch` chạy gateway ở chế độ theo dõi và tự động nạp lại khi có thay đổi trong file TypeScript.

### 2) Trỏ ứng dụng macOS vào Gateway đang chạy

Trong **Moltbot.app**:

- Chế độ kết nối (Connection Mode): **Local**
Ứng dụng sẽ tự động kết nối vào gateway đang chạy trên cổng (port) đã cấu hình.

### 3) Xác minh

- Trạng thái Gateway trong app sẽ báo **“Using existing gateway …”** (Đang dùng gateway có sẵn)
- Hoặc kiểm tra qua CLI:

```bash
moltbot health
```

### Các lỗi thường gặp
- **Sai cổng (Wrong port):** Gateway WebSocket mặc định là `ws://127.0.0.1:18789`; hãy đảm bảo app và CLI dùng chung một cổng.
- **Nơi lưu trữ dữ liệu:**
  - Thông tin đăng nhập (Credentials): `~/.clawdbot/credentials/`
  - Phiên làm việc (Sessions): `~/.clawdbot/agents/<agentId>/sessions/`
  - Nhật ký (Logs): `/tmp/moltbot/`

## Bản đồ lưu trữ thông tin đăng nhập (Credentials)

Sử dụng bản đồ này khi debug xác thực hoặc quyết định xem cần sao lưu những gì:

- **WhatsApp**: `~/.clawdbot/credentials/whatsapp/<accountId>/creds.json`
- **Telegram bot token**: config/env hoặc `channels.telegram.tokenFile`
- **Discord bot token**: config/env (chưa hỗ trợ file token)
- **Slack tokens**: config/env (`channels.slack.*`)
- **Danh sách phê duyệt ghép nối**: `~/.clawdbot/credentials/<channel>-allowFrom.json`
- **Cấu hình xác thực Model**: `~/.clawdbot/agents/<agentId>/agent/auth-profiles.json`
- **OAuth cũ**: `~/.clawdbot/credentials/oauth.json`
Chi tiết hơn: [Bảo mật](../gateway/security.vi.md#ban-do-luu-tru-thong-tin-dang-nhap).

## Cập nhật (Mà không phá hỏng thiết lập)

- Hãy giữ `~/clawd` và `~/.clawdbot/` là “của riêng bạn”; đừng đưa các câu lệnh prompts hay cấu hình cá nhân vào trong repo `moltbot`.
- Cập nhật mã nguồn: `git pull` + `pnpm install` (khi file lock thay đổi) + tiếp tục dùng `pnpm gateway:watch`.

## Linux (systemd user service)

Các bản cài đặt Linux sử dụng dịch vụ systemd ở cấp độ **user** (người dùng). Theo mặc định, systemd sẽ dừng các dịch vụ của người dùng khi đăng xuất hoặc máy rảnh (idle), điều này sẽ làm tắt Gateway. Trình hướng dẫn cài đặt sẽ cố gắng kích hoạt tính năng "lingering" (duy trì) cho bạn (có thể yêu cầu sudo). Nếu nó vẫn tắt, hãy chạy lệnh:

```bash
sudo loginctl enable-linger $USER
```

Đối với máy chủ luôn bật hoặc đa người dùng, hãy cân nhắc sử dụng dịch vụ cấp **system** (hệ thống) thay vì cấp user (không cần lingering). Xem [Sổ tay Gateway](../gateway/index.vi.md) để biết các ghi chú về systemd.

## Tài liệu liên quan

- [Sổ tay Gateway](../gateway/index.vi.md) (các cờ lệnh, giám sát, cổng kết nối)
- [Cấu hình Gateway](../gateway/configuration.vi.md) (sơ đồ cấu hình + ví dụ)
- [Discord](../channels/discord.vi.md) và [Telegram](../channels/telegram.vi.md) (tags phản hồi + thiết lập replyToMode)
- [Thiết lập trợ lý Moltbot](./clawd.vi.md)
- [Ứng dụng macOS](../platforms/macos.vi.md) (vòng đời gateway)
