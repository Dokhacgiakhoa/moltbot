---
summary: "Hướng dẫn cho người mới: từ số không đến tin nhắn đầu tiên (wizard, xác thực, các kênh, ghép nối)"
read_when:
  - Cài đặt lần đầu từ đầu
  - Muốn đi con đường nhanh nhất từ cài đặt → thiết lập ban đầu → tin nhắn đầu tiên
---

# Hướng dẫn Bắt đầu (Getting Started)

Mục tiêu: đi từ **số không** → **có cuộc trò chuyện đầu tiên** (với các cấu hình mặc định hợp lý) nhanh nhất có thể.

Cách chat nhanh nhất: mở Control UI (không cần thiết lập kênh). Chạy lệnh `moltbot dashboard` và chat trong trình duyệt, hoặc mở `http://127.0.0.1:18789/` trên máy chủ gateway.
Tùy chọn tài liệu: [Dashboard](../web/dashboard.vi.md) và [Control UI](../web/control-ui.vi.md).

Con đường khuyên dùng: sử dụng **trình hướng dẫn CLI (onboarding wizard)** (`moltbot onboard`). Nó sẽ thiết lập giúp bạn:
- model/auth (xác thực - khuyên dùng OAuth)
- cấu hình gateway
- các kênh (WhatsApp/Telegram/Discord/Mattermost (plugin)/...)
- mặc định ghép nối (secure DMs)
- khởi tạo không gian làm việc + kỹ năng (workspace + skills)
- dịch vụ chạy ngầm tùy chọn

Nếu bạn muốn xem các trang tham chiếu chuyên sâu hơn, hãy nhảy đến: [Wizard](./wizard.vi.md), [Thiết lập](./setup.vi.md), [Ghép nối](./pairing.vi.md), [Bảo mật](../gateway/security.vi.md).

Lưu ý về Sandboxing: `agents.defaults.sandbox.mode: "non-main"` sử dụng `session.mainKey` (mặc định là `"main"`), vì vậy các phiên (session) nhóm/kênh chat sẽ được đặt trong sandbox. Nếu bạn muốn agent chính luôn chạy trên host, hãy thiết lập ghi đè cụ thể cho từng agent:

```json
{
  "routing": {
    "agents": {
      "main": {
        "workspace": "~/clawd",
        "sandbox": { "mode": "off" }
      }
    }
  }
}
```

## 0) Điều kiện tiên quyết

- Node `>=22`
- `pnpm` (tùy chọn; khuyên dùng nếu bạn build từ mã nguồn)
- **Khuyên dùng:** API key của Brave Search để tìm kiếm web. Cách dễ nhất:
  `moltbot configure --section web` (lưu trữ `tools.web.search.apiKey`).
  Xem [Công cụ Web](../tools/web.vi.md).

macOS: nếu bạn định build app, hãy cài Xcode / CLT. Đối với CLI + gateway, chỉ cần Node là đủ.
Windows: hãy sử dụng **WSL2** (khuyên dùng Ubuntu). WSL2 cực kỳ được khuyến khích; chạy trực tiếp trên Windows (native) chưa được kiểm thử, nhiều lỗi hơn và khả năng tương thích công cụ kém hơn. Hãy cài WSL2 trước, sau đó thực hiện các bước Linux bên trong WSL. Xem [Windows (WSL2)](../platforms/windows.vi.md).

## 1) Cài đặt CLI (Khuyên dùng)

```bash
curl -fsSL https://molt.bot/install.sh | bash
```

Các tùy chọn cài đặt (phương thức cài đặt, không tương tác, từ GitHub): [Cài đặt](../install/index.vi.md).

Windows (PowerShell):

```powershell
iwr -useb https://molt.bot/install.ps1 | iex
```

Cách khác (cài đặt global qua npm):

```bash
npm install -g moltbot@latest
```

```bash
pnpm add -g moltbot@latest
```

## 2) Chạy trình hướng dẫn cài đặt (và cài đặt dịch vụ)

```bash
moltbot onboard --install-daemon
```

Những gì bạn sẽ chọn:
- Gateway **Local (cục bộ) hay Remote (từ xa)**
- **Auth (Xác thực)**: Gói thuê bao OpenAI (Codex) (OAuth) hoặc API keys. Với Anthropic, chúng tôi khuyên dùng API key; `claude setup-token` cũng được hỗ trợ.
- **Providers (Nhà cung cấp)**: Đăng nhập QR WhatsApp, bot tokens của Telegram/Discord, plugin tokens của Mattermost, v.v.
- **Daemon (Dịch vụ chạy ngầm)**: cài đặt nền (launchd/systemd; WSL2 dùng systemd)
  - **Runtime**: Node (khuyên dùng; bắt buộc đối với WhatsApp/Telegram). Bun **không được khuyên dùng**.
- **Gateway token**: trình hướng dẫn sẽ tự sinh một token mặc định và lưu trong `gateway.auth.token`.

Tài liệu về Wizard: [Wizard](./wizard.vi.md)

### Auth: nơi lưu trữ (quan trọng)

- **Cách dùng Anthropic khuyên dùng:** thiết lập một API key (wizard có thể lưu nó để dịch vụ sử dụng). `claude setup-token` cũng được hỗ trợ nếu bạn muốn dùng lại thông tin đăng nhập của Claude Code.

- Thông tin đăng nhập OAuth (legacy import): `~/.clawdbot/credentials/oauth.json`
- Cấu hình xác thực (OAuth + API keys): `~/.clawdbot/agents/<agentId>/agent/auth-profiles.json`

Mẹo cho máy chủ không có giao diện (headless): thực hiện OAuth trên máy bình thường trước, sau đó copy file `oauth.json` sang máy chủ gateway.

## 3) Khởi động Gateway

Nếu bạn đã cài đặt dịch vụ (service) trong quá trình onboarding, Gateway sẽ đã đang chạy rồi:

```bash
moltbot gateway status
```

Chạy thủ công (hiện nền):

```bash
moltbot gateway --port 18789 --verbose
```

Dashboard (local loopback): `http://127.0.0.1:18789/`
Nếu đã cài đặt token, hãy dán nó vào phần cài đặt Control UI (được lưu là `connect.params.auth.token`).

⚠️ **Cảnh báo về Bun (WhatsApp + Telegram):** Bun gặp một số lỗi đã biết với các kênh này. Nếu bạn dùng WhatsApp hoặc Telegram, hãy chạy Gateway bằng **Node**.

## 3.5) Kiểm tra nhanh (2 phút)

```bash
moltbot status
moltbot health
moltbot security audit --deep
```

## 4) Ghép nối + kết nối giao diện chat đầu tiên

### WhatsApp (Đăng nhập qua QR)

```bash
moltbot channels login
```

Quét mã qua WhatsApp → Cài đặt (Settings) → Thiết bị liên kết (Linked Devices).

Tài liệu WhatsApp: [WhatsApp](../channels/whatsapp.vi.md)

### Telegram / Discord / các kênh khác

Trình hướng dẫn có thể viết token/cấu hình giúp bạn. Nếu bạn thích cấu hình thủ công, hãy bắt đầu tại:
- Telegram: [Telegram](../channels/telegram.vi.md)
- Discord: [Discord](../channels/discord.vi.md)
- Mattermost (plugin): [Mattermost](../channels/mattermost.vi.md)

**Mẹo cho Telegram DM:** tin nhắn riêng đầu tiên của bạn sẽ nhận lại một mã ghép nối. Hãy phê duyệt nó (xem bước tiếp theo) nếu không bot sẽ không trả lời.

## 5) An toàn tin nhắn DM (phê duyệt ghép nối)

Chế độ mặc định: các tin nhắn DM từ người lạ sẽ nhận được một mã ngắn và tin nhắn không được xử lý cho đến khi được phê duyệt.
Nếu tin nhắn DM đầu tiên của bạn không có phản hồi, hãy phê duyệt ghép nối:

```bash
moltbot pairing list whatsapp
moltbot pairing approve whatsapp <code>
```

Tài liệu Ghép nối: [Pairing](./pairing.vi.md)

## Cài từ nguồn (dành cho phát triển)

Nếu bạn đang trực tiếp chỉnh sửa Moltbot, hãy chạy từ mã nguồn:

```bash
git clone https://github.com/moltbot/moltbot.git
cd moltbot
pnpm install
pnpm ui:build # tự động cài deps cho UI lần đầu chạy
pnpm build
moltbot onboard --install-daemon
```

Nếu bạn chưa có bản cài đặt global, hãy chạy bước onboarding qua `pnpm moltbot ...` từ trong repo.
`pnpm build` cũng đóng gói các tài sản A2UI; nếu bạn chỉ cần chạy bước đó, hãy dùng `pnpm canvas:a2ui:bundle`.

Chạy Gateway (từ repo này):

```bash
node moltbot.mjs gateway --port 18789 --verbose
```

## 7) Xác minh toàn trình (End-to-end)

Trong một terminal mới, gửi một tin nhắn thử nghiệm:

```bash
moltbot message send --target +15555550123 --message "Xin chào từ Moltbot"
```

Nếu `moltbot health` báo “no auth configured”, hãy quay lại wizard và thiết lập OAuth/key auth — agent sẽ không thể phản hồi nếu không có nó.

Mẹo: `moltbot status --all` là báo cáo debug ở chế độ chỉ đọc tốt nhất để copy-paste.
Health probes: `moltbot health` (hoặc `moltbot status --deep`) sẽ hỏi gateway đang chạy để lấy ảnh chụp trạng thái sức khỏe hệ thống.

## Các bước tiếp theo (tùy chọn, nhưng rất hay)

- App macOS trên menu bar + voice wake: [Ứng dụng macOS](../platforms/macos.vi.md)
- Các node iOS/Android (Canvas/camera/giọng nói): [Nodes](../nodes/index.vi.md)
- Truy cập từ xa (SSH tunnel / Tailscale Serve): [Truy cập từ xa](../gateway/remote.vi.md) và [Tailscale](../gateway/tailscale.vi.md)
- Các thiết lập VPN / Always-on: [Truy cập từ xa](../gateway/remote.vi.md), [exe.dev](../platforms/exe-dev.vi.md), [Hetzner](../platforms/hetzner.vi.md), [macOS remote](../platforms/mac/remote.vi.md)
