---
summary: "Cài đặt Moltbot (bản cài đặt khuyên dùng, cài đặt global, hoặc từ mã nguồn)"
read_when:
  - Cài đặt Moltbot
  - Muốn cài đặt trực tiếp từ GitHub
---

# Cài đặt (Install)

Hãy sử dụng trình cài đặt (installer) trừ khi bạn có lý do cụ thể để làm khác. Nó sẽ thiết lập CLI và khởi chạy quá trình thiết lập ban đầu (onboarding).

## Cài đặt nhanh (Khuyên dùng)

```bash
curl -fsSL https://molt.bot/install.sh | bash
```

Windows (PowerShell):

```powershell
iwr -useb https://molt.bot/install.ps1 | iex
```

Bước tiếp theo (nếu bạn đã bỏ qua phần onboarding):

```bash
moltbot onboard --install-daemon
```

## Yêu cầu hệ thống

- **Node >=22**
- macOS, Linux, hoặc Windows thông qua WSL2
- `pnpm` (chỉ cần nếu bạn cài đặt từ mã nguồn)

## Lựa chọn phương thức cài đặt

### 1) Kịch bản cài đặt (Khuyên dùng)

Tự động cài đặt `moltbot` global qua npm và chạy onboarding.

```bash
curl -fsSL https://molt.bot/install.sh | bash
```

Các cờ lệnh của trình cài đặt:

```bash
curl -fsSL https://molt.bot/install.sh | bash -s -- --help
```

Chi tiết: [Cơ chế bên trong trình cài đặt](./installer.vi.md).

Chế độ không tương tác (bỏ qua onboarding):

```bash
curl -fsSL https://molt.bot/install.sh | bash -s -- --no-onboard
```

### 2) Cài đặt Global (Thủ công)

Nếu bạn đã cài sẵn Node:

```bash
npm install -g moltbot@latest
```

Nếu bạn đã cài `libvips` trên toàn hệ thống (phổ biến trên macOS qua Homebrew) và việc cài đặt thư viện `sharp` gặp lỗi, hãy ép buộc sử dụng các tệp nhị phân build sẵn:

```bash
SHARP_IGNORE_GLOBAL_LIBVIPS=1 npm install -g moltbot@latest
```

Nếu gặp lỗi `sharp: Please add node-gyp to your dependencies`, hãy cài đặt các công cụ build (macOS: Xcode CLT + `npm install -g node-gyp`) hoặc dùng cách `SHARP_IGNORE_GLOBAL_LIBVIPS=1` ở trên để bỏ qua bước build native.

Hoặc dùng pnpm:

```bash
pnpm add -g moltbot@latest
```

Sau đó:

```bash
moltbot onboard --install-daemon
```

### 3) Cài đặt từ mã nguồn (Dành cho Dev/Người đóng góp)

```bash
git clone https://github.com/moltbot/moltbot.git
cd moltbot
pnpm install
pnpm ui:build # tự động cài đặt deps cho UI ở lần chạy đầu tiên
pnpm build
moltbot onboard --install-daemon
```

Mẹo: nếu bạn chưa cài bản global, hãy chạy các lệnh trong repo qua `pnpm moltbot ...`.

### 4) Các tùy chọn cài đặt khác

- Docker: [Docker](./docker.vi.md)
- Nix: [Nix](./nix.vi.md)
- Ansible: [Ansible](./ansible.vi.md)
- Bun (Chỉ dành cho CLI): [Bun](./bun.vi.md)

## Sau khi cài đặt

- Chạy onboarding: `moltbot onboard --install-daemon`
- Kiểm tra nhanh: `moltbot doctor`
- Kiểm tra sức khỏe gateway: `moltbot status` + `moltbot health`
- Mở bảng điều khiển: `moltbot dashboard`

## Phương thức cài đặt: npm vs git (installer)

Trình cài đặt hỗ trợ hai phương thức:

- `npm` (mặc định): `npm install -g moltbot@latest`
- `git`: clone/build từ GitHub và chạy trực tiếp từ thư mục mã nguồn

### Các cờ lệnh CLI

```bash
# Cài đặt qua npm rõ ràng
curl -fsSL https://molt.bot/install.sh | bash -s -- --install-method npm

# Cài đặt từ GitHub (source checkout)
curl -fsSL https://molt.bot/install.sh | bash -s -- --install-method git
```

Các cờ lệnh phổ biến:

- `--install-method npm|git`
- `--git-dir <đường_dẫn>` (mặc định: `~/moltbot`)
- `--no-git-update` (bỏ qua `git pull` khi sử dụng thư mục đã có sẵn)
- `--no-prompt` (tắt các yêu cầu nhập liệu; cần thiết cho CI/tự động hóa)
- `--dry-run` (chỉ in ra những gì sẽ thực hiện; không thay đổi hệ thống)
- `--no-onboard` (bỏ qua thiết lập ban đầu)

### Biến môi trường

Các biến môi trường tương đương (hữu ích cho tự động hóa):

- `CLAWDBOT_INSTALL_METHOD=git|npm`
- `CLAWDBOT_GIT_DIR=...`
- `CLAWDBOT_GIT_UPDATE=0|1`
- `CLAWDBOT_NO_PROMPT=1`
- `CLAWDBOT_DRY_RUN=1`
- `CLAWDBOT_NO_ONBOARD=1`
- `SHARP_IGNORE_GLOBAL_LIBVIPS=0|1` (mặc định: `1`; để tránh `sharp` build bằng hệ thống libvips)

## Khắc phục lỗi: Không tìm thấy lệnh `moltbot` (PATH)

Kiểm tra nhanh:

```bash
node -v
npm -v
npm prefix -g
echo "$PATH"
```

Nếu `$(npm prefix -g)/bin` (macOS/Linux) hoặc `$(npm prefix -g)` (Windows) **không** xuất hiện trong kết quả `echo "$PATH"`, shell của bạn sẽ không tìm thấy các file thực thi global của npm (bao gồm cả `moltbot`).

Cách sửa: thêm nó vào file khởi động shell của bạn (zsh: `~/.zshrc`, bash: `~/.bashrc`):

```bash
# macOS / Linux
export PATH="$(npm prefix -g)/bin:$PATH"
```

Trên Windows, hãy thêm đầu ra của lệnh `npm prefix -g` vào biến môi trường PATH của hệ thống.

Sau đó mở một terminal mới (hoặc chạy `rehash` trong zsh / `hash -r` trong bash).

## Cập nhật / Gỡ cài đặt

- Cập nhật: [Updating](./updating.vi.md)
- Chuyển sang máy mới: [Migrating](./migrating.vi.md)
- Gỡ cài đặt: [Uninstall](./uninstall.vi.md)
