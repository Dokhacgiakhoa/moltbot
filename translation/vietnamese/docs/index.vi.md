---
summary: "Tổng quan về Moltbot, các tính năng và mục đích sử dụng"
read_when:
  - Giới thiệu Moltbot cho người mới bắt đầu
---
# Moltbot 🦞

> *"LỘT XÁC! LỘT XÁC!"* — Một chú tôm hùm không gian, chắc vậy.

<p align="center">
  <img src="whatsapp-clawd.jpg" alt="Moltbot" width="420" />
</p>

<p align="center">
  <strong>Cổng kết nối AI cho mọi hệ điều hành + WhatsApp/Telegram/Discord/iMessage.</strong><br />
  Các Plugin bổ sung thêm Mattermost và nhiều hơn nữa.<br />
  Gửi một tin nhắn, nhận phản hồi từ Agent — ngay trong túi của bạn.
</p>

<p align="center">
  <a href="https://github.com/moltbot/moltbot">GitHub</a> ·
  <a href="https://github.com/moltbot/moltbot/releases">Bản phát hành</a> ·
  <a href="/">Tài liệu</a> ·
  <a href="/start/clawd.vi.md">Thiết lập trợ lý Moltbot</a>
</p>

Moltbot kết nối WhatsApp (qua WhatsApp Web / Baileys), Telegram (Bot API / grammY), Discord (Bot API / discord.js), và iMessage (imsg CLI) tới các Agent lập trình như [Pi](https://github.com/badlogic/pi-mono). Các Plugin bổ sung thêm Mattermost và nhiều nền tảng khác. Moltbot cũng là nền tảng vận hành [Clawd](https://clawd.me), chú trợ lý tôm hùm không gian.

## Bắt đầu tại đây

- **Cài đặt mới từ đầu:** [Hướng dẫn bắt đầu](../start/getting-started.vi.md)
- **Thiết lập theo hướng dẫn (khuyên dùng):** [Trình hướng dẫn - Wizard](../start/wizard.vi.md) (`moltbot onboard`)
- **Mở bảng điều khiển (Local Gateway):** http://localhost:18789/

Nếu Gateway đang chạy trên máy tính của bạn, liên kết trên sẽ mở giao diện điều khiển (Control UI) ngay lập tức. Nếu không tải được, hãy khởi động Gateway trước bằng lệnh: `moltbot gateway`.

## Bảng điều khiển (Giao diện điều khiển Web)

Bảng điều khiển là nơi bạn có thể trò chuyện, cấu hình hệ thống, quản lý nút mạng và các phiên làm việc.
- Địa chỉ cục bộ: http://127.0.0.1:18789/
- Truy cập từ xa: [Bề mặt giao diện Web](../web/index.vi.md) và [Tailscale](../gateway/tailscale.vi.md)

## Cơ chế hoạt động

Hầu hết các hoạt động đều đi qua **Gateway** (`moltbot gateway`), một tiến trình chạy ngầm duy nhất quản lý các kết nối kênh nhắn tin và quyền điều khiển WebSocket.

## Mô hình mạng

- **Mỗi máy chủ một Gateway (khuyên dùng)**: Đây là tiến trình duy nhất được phép quản lý phiên WhatsApp Web.
- **Ưu tiên nội bộ (Loopback)**: WebSocket của Gateway mặc định chạy tại `ws://127.0.0.1:18789`.
- **Nút mạng (Nodes)**: Kết nối tới Gateway qua mạng nội bộ, Tailscale hoặc SSH.
- **Truy cập từ xa**: Sử dụng SSH tunnel hoặc Tailscale; xem [Truy cập từ xa](../gateway/remote.vi.md).

## Các tính năng chính (Tóm tắt)

- 📱 **Tích hợp WhatsApp** — Sử dụng giao thức WhatsApp Web.
- ✈️ **Bot Telegram** — Chat riêng tư (DM) + Nhóm qua Bot API.
- 🎮 **Bot Discord** — Chat riêng tư + Các kênh trong máy chủ.
- 💬 **iMessage** — Tích hợp qua công cụ dòng lệnh trên macOS.
- 🤖 **Cầu nối Agent** — Kết nối với Pi (chế độ RPC) với khả năng truyền phát dữ liệu.
- 🧠 **Điều hướng đa Agent** — Phân chia tài khoản/người dùng cho các Agent riêng biệt (cách ly không gian làm việc).
- 🔐 **Xác thực thuê bao** — Hỗ trợ Anthropic (Claude Pro/Max) + OpenAI (ChatGPT/Codex) qua OAuth.
- 👥 **Hỗ trợ Chat nhóm** — Mặc định dựa trên việc nhắc tên (@mention).
- 📎 **Hỗ trợ Đa phương tiện** — Gửi và nhận hình ảnh, âm thanh, tài liệu.
- 🖥️ **WebChat & App macOS** — Giao diện cục bộ và ứng dụng trên thanh menu.

## Bắt đầu nhanh

Yêu cầu hệ thống: **Node ≥ 22**.

```bash
# Cài đặt qua npm (khuyên dùng)
npm install -g moltbot@latest

# Thiết lập và cài đặt dịch vụ chạy ngầm
moltbot onboard --install-daemon

# Đăng nhập WhatsApp (hiển thị mã QR)
moltbot channels login
```

---

## Tài liệu chi tiết

- **Trung tâm hướng dẫn**:
  - [Trung tâm trợ giúp](./help/index.vi.md) ← *Cách sửa lỗi & Xử lý sự cố*
  - [Cấu hình hệ thống](./gateway/configuration.vi.md)
  - [Các lệnh dòng lệnh (Slash commands)](./tools/slash-commands.vi.md)
  - [Điều hướng đa Agent](./concepts/multi-agent.vi.md)
  - [Cập nhật & Quay lại phiên bản cũ](./install/updating.vi.md)
  - [Quản lý Nút mạng (iOS/Android)](./nodes/index.vi.md)
  - [Giao diện Web (Control UI)](./web/index.vi.md)

## Bản quyền

MIT — Tự do như chú tôm hùm giữa đại dương 🦞
