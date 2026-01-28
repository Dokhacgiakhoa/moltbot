---
summary: "Gỡ cài đặt Moltbot hoàn toàn (CLI, dịch vụ, trạng thái, không gian làm việc)"
read_when:
  - Bạn muốn xóa Moltbot khỏi máy tính
  - Dịch vụ gateway vẫn đang chạy sau khi gỡ cài đặt
---

# Gỡ cài đặt (Uninstall)

Có hai cách:
- **Cách đơn giản** nếu `moltbot` vẫn còn được cài đặt.
- **Xóa dịch vụ thủ công** nếu CLI đã bị xóa nhưng dịch vụ vẫn đang chạy.

## Cách đơn giản (CLI vẫn còn)

Khuyên dùng: sử dụng trình gỡ cài đặt tích hợp sẵn:

```bash
moltbot uninstall
```

Chế độ không tương tác (cho tự động hóa / npx):

```bash
moltbot uninstall --all --yes --non-interactive
npx -y moltbot uninstall --all --yes --non-interactive
```

Các bước thủ công (kết quả tương đương):

1) Dừng dịch vụ gateway:

```bash
moltbot gateway stop
```

2) Gỡ cài đặt dịch vụ gateway (launchd/systemd/schtasks):

```bash
moltbot gateway uninstall
```

3) Xóa trạng thái + cấu hình:

```bash
rm -rf "${CLAWDBOT_STATE_DIR:-$HOME/.clawdbot}"
```

Nếu bạn thiết lập `CLAWDBOT_CONFIG_PATH` ở một vị trí khác, hãy xóa cả file đó.

4) Xóa không gian làm việc (tùy chọn, sẽ xóa các file của agent):

```bash
rm -rf ~/clawd
```

5) Gỡ bỏ cài đặt CLI (chọn lệnh tương ứng với trình quản lý gói bạn đã dùng):

```bash
npm rm -g moltbot
pnpm remove -g moltbot
bun remove -g moltbot
```

6) Nếu bạn đã cài ứng dụng macOS:

```bash
rm -rf /Applications/Moltbot.app
```

## Xóa dịch vụ thủ công (CLI đã bị xóa)

Sử dụng cách này nếu dịch vụ gateway vẫn chạy nhưng lệnh `moltbot` không còn tồn tại.

### macOS (launchd)

Tên mặc định là `bot.molt.gateway`:

```bash
launchctl bootout gui/$UID/bot.molt.gateway
rm -f ~/Library/LaunchAgents/bot.molt.gateway.plist
```

### Linux (systemd user unit)

Tên mặc định là `moltbot-gateway.service`:

```bash
systemctl --user disable --now moltbot-gateway.service
rm -f ~/.config/systemd/user/moltbot-gateway.service
systemctl --user daemon-reload
```

### Windows (Scheduled Task)

Tên mặc định là `Moltbot Gateway`.
File kịch bản của tác vụ nằm trong thư mục trạng thái của bạn.

```powershell
schtasks /Delete /F /TN "Moltbot Gateway"
Remove-Item -Force "$env:USERPROFILE\.clawdbot\gateway.cmd"
```

## Cài đặt thông thường vs Chạy từ mã nguồn

### Cài đặt thông thường (install.sh / npm / pnpm / bun)

Nếu bạn đã dùng `https://molt.bot/install.sh` hoặc `install.ps1`, CLI đã được cài đặt qua `npm install -g moltbot@latest`.
Hãy gỡ bỏ bằng `npm rm -g moltbot`.

### Chạy từ mã nguồn (git clone)

Nếu bạn chạy trực tiếp từ repo đã clone:

1) Gỡ cài đặt dịch vụ gateway **trước khi** xóa repo.
2) Xóa thư mục repo.
3) Xóa trạng thái + không gian làm việc như hướng dẫn ở trên.
