---
summary: "Trình hướng dẫn thiết lập CLI (CLI onboarding wizard): hướng dẫn thiết lập gateway, không gian làm việc, các kênh và kỹ năng"
read_when:
  - Chạy hoặc cấu hình trình hướng dẫn thiết lập ban đầu
  - Thiết lập trên một máy mới
---

# Trình hướng dẫn Thiết lập (CLI Wizard)

Trình hướng dẫn thiết lập (onboarding wizard) là cách **được khuyên dùng** để cài đặt Moltbot trên macOS, Linux, hoặc Windows (thông qua WSL2; cực kỳ khuyến khích).
Nó sẽ giúp cấu hình Gateway cục bộ hoặc kết nối Gateway từ xa, cùng với các kênh, kỹ năng và không gian làm việc mặc định trong một quy trình hướng dẫn duy nhất.

Lối vào chính:

```bash
moltbot onboard
```

Cách chat nhanh nhất: mở Control UI (không cần thiết lập kênh). Chạy lệnh `moltbot dashboard` và chat trong trình duyệt. Tài liệu: [Dashboard](../web/dashboard.vi.md).

Tái cấu hình sau này:

```bash
moltbot configure
```

Khuyên dùng: thiết lập API key của Brave Search để agent có thể dùng lệnh `web_search` (`web_fetch` vẫn hoạt động mà không cần key). Cách dễ nhất: `moltbot configure --section web`, lệnh này sẽ lưu vào `tools.web.search.apiKey`. Tài liệu: [Công cụ Web](../tools/web.vi.md).

## QuickStart (Bắt đầu nhanh) vs Advanced (Nâng cao)

Trình hướng dẫn bắt đầu bằng việc chọn **QuickStart** (dùng mặc định) vs **Advanced** (toàn quyền kiểm soát).

**QuickStart** sẽ giữ các mặc định sau:
- Gateway cục bộ (loopback)
- Không gian làm việc mặc định (hoặc không gian hiện có)
- Cổng Gateway **18789**
- Xác thực Gateway dùng **Token** (tự động tạo, kể cả trên loopback)
- Công khai qua Tailscale: **Tắt**
- Tin nhắn DM trên Telegram + WhatsApp mặc định là **danh sách phê duyệt (allowlist)** (bạn sẽ được hỏi số điện thoại)

**Advanced** sẽ hiển thị mọi bước (chế độ, không gian làm việc, gateway, các kênh, dịch vụ chạy ngầm, kỹ năng).

## Trình hướng dẫn làm những gì?

**Chế độ Local (mặc định)** sẽ dẫn dắt bạn qua:
- Model/Auth (Xác thực): Đăng ký OpenAI Code (Codex) OAuth, Anthropic API key (khuyên dùng) hoặc setup-token (dán mã), cùng các lựa chọn MiniMax/GLM/Moonshot/AI Gateway.
- Vị trí không gian làm việc (Workspace) + các file khởi tạo ban đầu.
- Thiết lập Gateway (cổng/bind/xác thực/tailscale).
- Nhà cung cấp (Providers): Telegram, WhatsApp, Discord, Google Chat, Mattermost (plugin), Signal.
- Cài đặt dịch vụ chạy ngầm (LaunchAgent / systemd user unit).
- Kiểm tra sức khỏe hệ thống.
- Kỹ năng (Khuyên dùng).

**Chế độ Remote** chỉ cấu hình client cục bộ để kết nối đến một Gateway ở nơi khác. Nó **không** cài đặt hay thay đổi bất cứ gì trên máy chủ từ xa.

Để thêm các agent riêng biệt khác (không gian làm việc + phiên làm việc + xác thực riêng), hãy dùng:

```bash
moltbot agents add <tên>
```

Mẹo: cờ `--json` **không** có nghĩa là chế độ không tương tác. Hãy dùng `--non-interactive` (và `--workspace`) cho các kịch bản script.

## Chi tiết quy trình (Bản cục bộ)

1) **Phát hiện cấu hình hiện có**
   - Nếu file `~/.clawdbot/moltbot.json` đã tồn tại, hãy chọn **Keep (Giữ) / Modify (Sửa) / Reset (Đặt lại)**.
   - Chạy lại trình hướng dẫn sẽ **không** xóa gì trừ khi bạn chọn **Reset** rõ ràng (hoặc dùng cờ `--reset`).
   - Nếu cấu hình không hợp lệ hoặc chứa các khóa cũ, trình hướng dẫn sẽ dừng lại và yêu cầu bạn chạy `moltbot doctor` trước khi tiếp tục.
   - Reset sử dụng lệnh `trash` (thùng rác) thay vì `rm` và cung cấp các phạm vi:
     - Chỉ cấu hình
     - Cấu hình + thông tin đăng nhập + các phiên làm việc
     - Đặt lại hoàn toàn (xóa cả không gian làm việc)

2) **Model/Auth (Mô hình/Xác thực)**
   - **Anthropic API key (khuyên dùng)**: dùng biến `ANTHROPIC_API_KEY` nếu có hoặc yêu cầu nhập key, sau đó lưu lại để dịch vụ chạy ngầm sử dụng.
   - **Anthropic OAuth (Claude Code CLI)**: trên macOS, wizard kiểm tra mục Keychain "Claude Code-credentials"; trên Linux/Windows, nó dùng lại `~/.claude/.credentials.json` nếu có.
   - **Mã Anthropic (Dán setup-token)**: chạy `claude setup-token` trên bất kỳ máy nào, sau đó dán mã vào.
   - **OpenAI Code (Codex) (OAuth)**: quy trình qua trình duyệt; dán mã `code#state`.
     - Thiết lập `agents.defaults.model` thành `openai-codex/gpt-5.2`.
   - **OpenAI API key**: dùng biến `OPENAI_API_KEY` nếu có hoặc yêu cầu nhập key, sau đó lưu vào `~/.clawdbot/.env`.
   - **Skip (Bỏ qua)**: chưa thiết lập xác thực.
   - Chọn một mô hình mặc định từ các tùy chọn được phát hiện.
   - Wizard sẽ kiểm tra mô hình và cảnh báo nếu mô hình không xác định hoặc thiếu xác thực.
   - Thông tin OAuth nằm ở `~/.clawdbot/credentials/oauth.json`; hồ sơ xác thực nằm ở `~/.clawdbot/agents/<agentId>/agent/auth-profiles.json`.
   - Chi tiết: [Khái niệm OAuth](../concepts/oauth.vi.md)

3) **Không gian làm việc (Workspace)**
   - Mặc định là `~/clawd` (có thể cấu hình).
   - Khởi tạo các file cần thiết cho nghi thức khởi động agent.
   - Sơ đồ không gian làm việc + hướng dẫn sao lưu: [Workspace của Agent](../concepts/agent-workspace.vi.md)

4) **Gateway**
   - Cổng (Port), bind, chế độ xác thực, công khai tailscale.
   - Khuyến nghị xác thực: hãy giữ chế độ **Token** kể cả trên loopback để các client WebSocket cục bộ bắt buộc phải xác thực.

5) **Kênh (Channels)**
   - WhatsApp: đăng nhập tùy chọn qua QR.
   - Telegram/Discord: mã Token của bot.
   - Google Chat: file JSON tài khoản dịch vụ.
   - An toàn DM: mặc định là ghép nối (pairing). Tin nhắn DM đầu tiên sẽ gửi một mã; phê duyệt qua lệnh `moltbot pairing approve <kênh> <mã>`.

6) **Cài đặt dịch vụ chạy ngầm (Daemon)**
   - macOS: LaunchAgent.
   - Linux (và Windows qua WSL2): systemd user unit.
     - Wizard sẽ cố gắng kích hoạt tính năng duy trì (lingering) qua `loginctl enable-linger <user>` để Gateway vẫn chạy sau khi bạn đăng xuất.
   - **Lựa chọn Runtime:** Node (khuyên dùng; bắt buộc cho WhatsApp/Telegram). Bun **không được khuyên dùng**.

7) **Kiểm tra sức khỏe (Health check)**
   - Khởi động Gateway (nếu cần) và chạy `moltbot health`.

8) **Kỹ năng (Skills - khuyên dùng)**
   - Đọc các kỹ năng có sẵn và kiểm tra yêu cầu.
   - Cho phép bạn chọn trình quản lý node: **npm / pnpm**.

9) **Hoàn tất**
   - Tóm tắt + các bước tiếp theo, bao gồm link tải app iOS/Android/macOS.

## Chế độ Remote (Từ xa)

Chế độ Remote cấu hình client cục bộ để kết nối đến một Gateway ở nơi khác.
Những gì bạn sẽ thiết lập:
- URL Gateway từ xa (`ws://...`)
- Token nếu Gateway yêu cầu xác thực (khuyên dùng)

Lưu ý:
- Không có việc cài đặt hay thay đổi dịch vụ nào được thực hiện từ xa.
- Nếu Gateway chỉ cho phép loopback, hãy dùng SSH tunneling hoặc tailnet.

## Thêm agent khác

Dùng `moltbot agents add <tên>` để tạo một agent riêng biệt với không gian làm việc, các phiên và hồ sơ xác thực riêng. Chạy mà không có cờ `--workspace` sẽ khởi chạy wizard.

## Chế độ không tương tác (Non‑interactive)

Sử dụng `--non-interactive` để tự động hóa việc thiết lập:

```bash
moltbot onboard --non-interactive \
  --mode local \
  --auth-choice apiKey \
  --anthropic-api-key "$ANTHROPIC_API_KEY" \
  --install-daemon \
  --daemon-runtime node
```

## Thiết lập Signal (signal-cli)

Wizard có thể cài đặt `signal-cli` từ GitHub:
- Tải về bản phát hành phù hợp.
- Lưu vào `~/.clawdbot/tools/signal-cli/<phiên_bản>/`.
- Ghi khóa `channels.signal.cliPath` vào cấu hình của bạn.

---
Tài liệu liên quan: [Cấu hình Gateway](../gateway/configuration.vi.md), [WhatsApp](../channels/whatsapp.vi.md), [Kỹ năng](../tools/skills.vi.md).
