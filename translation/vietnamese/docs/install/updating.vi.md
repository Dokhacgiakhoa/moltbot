---
summary: "Cập nhật Moltbot an toàn (cài đặt global hoặc từ nguồn), kèm theo chiến lược khôi phục (rollback)"
read_when:
  - Cập nhật Moltbot
  - Gặp lỗi sau khi cập nhật
---

# Cập nhật (Updating)

Moltbot đang phát triển rất nhanh (giai đoạn tiền “1.0”). Hãy coi các bản cập nhật như việc vận hành hạ tầng: cập nhật → chạy kiểm tra → khởi động lại (hoặc dùng `moltbot update`, lệnh này tự khởi động lại giúp bạn) → xác minh.

## Khuyên dùng: Chạy lại kịch bản cài đặt (nâng cấp tại chỗ)

Con đường cập nhật **được ưu tiên** là chạy lại trình cài đặt từ website. Nó sẽ tự động phát hiện bản cài đặt cũ, nâng cấp tại chỗ và chạy `moltbot doctor` khi cần thiết.

```bash
curl -fsSL https://molt.bot/install.sh | bash
```

Ghi chú:
- Thêm cờ `--no-onboard` nếu bạn không muốn chạy lại trình hướng dẫn thiết lập ban đầu.
- Đối với **cài đặt từ nguồn (source install)**, hãy dùng:
  ```bash
  curl -fsSL https://molt.bot/install.sh | bash -s -- --install-method git --no-onboard
  ```
  Trình cài đặt sẽ chạy `git pull --rebase` **chỉ khi** thư mục làm việc của bạn sạch sẽ (không có thay đổi chưa commit).
- Đối với **cài đặt global**, kịch bản này sử dụng lệnh `npm install -g moltbot@latest`.
- Ghi chú về tính tương thích: lệnh `moltbot` vẫn được duy trì như một lớp tương thích.

## Trước khi bạn cập nhật

- Hãy biết rõ bạn đã cài đặt theo cách nào: **global** (npm/pnpm) hay **từ mã nguồn** (git clone).
- Hãy biết rõ Gateway đang chạy thế nào: **trong terminal hiện nền** hay **dưới dạng dịch vụ (service)** (launchd/systemd).
- Sao lưu cấu hình cá nhân:
  - Cấu hình: `~/.clawdbot/moltbot.json`
  - Thông tin đăng nhập: `~/.clawdbot/credentials/`
  - Không gian làm việc (Workspace): `~/clawd`

## Cập nhật (Cài đặt Global)

Cập nhật bản global (chọn một):

```bash
npm i -g moltbot@latest
```

```bash
pnpm add -g moltbot@latest
```
Chúng tôi **không** khuyên dùng Bun cho runtime của Gateway (do các lỗi với WhatsApp/Telegram).

Để chuyển đổi giữa các kênh cập nhật (áp dụng cho cả bản cài qua git và npm):

```bash
moltbot update --channel beta
moltbot update --channel dev
moltbot update --channel stable
```

Sử dụng cờ `--tag <tag|phiên_bản>` nếu bạn muốn cài đặt một thẻ hoặc phiên bản cụ thể.

Xem [Các kênh phát triển](./development-channels.vi.md) để biết ý nghĩa các kênh và ghi chú phát hành.

Ghi chú: Với bản cài qua npm, gateway sẽ thông báo gợi ý cập nhật khi khởi động (kiểm tra dựa trên thẻ kênh hiện tại). Tắt tính năng này qua: `update.checkOnStart: false`.

Sau đó chạy:

```bash
moltbot doctor
moltbot gateway restart
moltbot health
```

Ghi chú:
- Nếu Gateway chạy như một dịch vụ, lệnh `moltbot gateway restart` được ưu tiên hơn việc tắt PID thủ công.
- Nếu bạn muốn cố định ở một phiên bản cụ thể, hãy xem phần “Khôi phục / Cố định phiên bản” bên dưới.

## Cập nhật (Dùng lệnh `moltbot update`)

Đối với **cài đặt từ nguồn** (git checkout), hãy ưu tiên dùng:

```bash
moltbot update
```

Lệnh này thực hiện quy trình cập nhật an toàn:
- Yêu cầu thư mục làm việc (worktree) sạch sẽ.
- Chuyển sang kênh đã chọn (thẻ hoặc nhánh).
- Fetch + rebase với nhánh thượng nguồn (upstream) đã cấu hình.
- Cài đặt dependencies, build dự án, build Control UI, và chạy `moltbot doctor`.
- Mặc định khởi động lại gateway (dùng `--no-restart` để bỏ qua).

Nếu bạn cài qua **npm/pnpm** (không có metadata của git), `moltbot update` sẽ cố gắng cập nhật qua trình quản lý gói của bạn. Nếu không phát hiện được, hãy dùng cách “Cập nhật (Cài đặt Global)” ở trên.

## Cập nhật (Qua Control UI / RPC)

Giao diện bảng điều khiển (Control UI) có nút **Update & Restart** (Cập nhật & Khởi động lại). Nó sẽ:
1) Thực hiện quy trình cập nhật nguồn tương tự như `moltbot update` (chỉ dành cho bản git checkout).
2) Ghi lại báo cáo kết quả cập nhật.
3) Khởi động lại gateway và thông báo kết quả cho phiên làm việc cuối cùng.

Nếu quá trình rebase thất bại, gateway sẽ hủy bỏ và khởi động lại mà không áp dụng bản cập nhật.

## Cập nhật (Từ mã nguồn)

Từ thư mục repo đã clone:

Cách khuyên dùng:

```bash
moltbot update
```

Cách thủ công (tương đương):

```bash
git pull
pnpm install
pnpm build
pnpm ui:build # tự động cài deps cho UI lần đầu chạy
moltbot doctor
moltbot health
```

Ghi chú:
- `pnpm build` rất quan trọng khi bạn chạy file nhị phân `moltbot` đóng gói ([`moltbot.mjs`](https://github.com/moltbot/moltbot/blob/main/moltbot.mjs)) hoặc dùng Node chạy thư mục `dist/`.
- Nếu bạn chạy trực tiếp từ TypeScript (`pnpm moltbot ...`), việc rebuild thường là không cần thiết, nhưng **vẫn cần chạy config migration** → hãy chạy `doctor`.
- Việc chuyển đổi giữa cài đặt global và cài từ git rất đơn giản: cài đặt kiểu còn lại, sau đó chạy `moltbot doctor` để gateway service trỏ về bản cài mới nhất.

## Luôn chạy: `moltbot doctor`

Doctor là lệnh "cập nhật an toàn". Nó được thiết kế để thực hiện các việc: sửa lỗi + di chuyển cấu hình + cảnh báo rủi ro.

Ghi chú: nếu bạn đang dùng **bản cài từ nguồn** (git checkout), `moltbot doctor` sẽ đề xuất chạy `moltbot update` trước.

Những việc điển hình mà doctor thực hiện:
- Di chuyển các khóa cấu hình cũ hoặc vị trí lưu file cấu hình cũ.
- Kiểm tra chính sách DM và cảnh báo các thiết lập rủi ro.
- Kiểm tra sức khỏe Gateway và đề xuất khởi động lại nếu cần.
- Phát hiện và di chuyển các dịch vụ gateway cũ (launchd/systemd...) sang các dịch vụ Moltbot hiện tại.
- Trên Linux, đảm bảo tính năng systemd user lingering hoạt động (để Gateway không bị tắt khi bạn log out).

Chi tiết: [Doctor](../gateway/doctor.vi.md)

## Bật / Tắt / Khởi động lại Gateway

CLI (hoạt động trên mọi hệ điều hành):

```bash
moltbot gateway status
moltbot gateway stop
moltbot gateway restart
moltbot gateway --port 18789
moltbot logs --follow
```

Nếu bạn chạy dưới dạng dịch vụ:
- macOS launchd: `launchctl kickstart -k gui/$UID/bot.molt.gateway`
- Linux systemd user service: `systemctl --user restart moltbot-gateway[-<profile>].service`
- Windows (WSL2): `systemctl --user restart moltbot-gateway[-<profile>].service`
- Lưu ý: Các lệnh dịch vụ chỉ hoạt động nếu dịch vụ đã được cài đặt; nếu chưa, hãy chạy `moltbot gateway install`.

Sổ tay hướng dẫn + tên các service: [Sổ tay Gateway](../gateway/index.vi.md)

## Khôi phục / Cố định phiên bản (Khi gặp lỗi)

### Cố định (Cài đặt Global)

Cài đặt một phiên bản cụ thể đã biết là hoạt động tốt (thay `<version>` bằng phiên bản đó):

```bash
npm i -g moltbot@<version>
```

```bash
pnpm add -g moltbot@<version>
```

Mẹo: để xem phiên bản hiện tại đã phát hành, chạy `npm view moltbot version`.

Sau đó khởi động lại và chạy lại doctor:

```bash
moltbot doctor
moltbot gateway restart
```

### Cố định (Từ nguồn) theo ngày

Chọn một commit theo ngày (Ví dụ: "trạng thái nhánh main vào ngày 01/01/2026"):

```bash
git fetch origin
git checkout "$(git rev-list -n 1 --before=\"2026-01-01\" origin/main)"
```

Sau đó cài lại deps + restart:

```bash
pnpm install
pnpm build
moltbot gateway restart
```

Nếu bạn muốn quay lại bản mới nhất sau này:

```bash
git checkout main
git pull
```

## Nếu bạn bị kẹt

- Hãy chạy `moltbot doctor` lần nữa và đọc kỹ kết quả (nó thường hướng dẫn cách sửa).
- Kiểm tra: [Khắc phục lỗi](../gateway/troubleshooting.vi.md)
- Hỏi trên Discord: https://channels.discord.gg/clawd
