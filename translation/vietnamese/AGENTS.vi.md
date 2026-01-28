# Hướng dẫn về Repository và Agents

- **Link Repo:** https://github.com/moltbot/moltbot
- **Giao tiếp trên GitHub:** Khi comment trên Issues hoặc PR, hãy dùng chuỗi nhiều dòng (literal multiline strings) hoặc `-F - <<'EOF'` (hoặc `$'...'`) để tạo dòng mới thực sự. Tuyệt đối không nhúng ký tự `\n` vào chuỗi.

## Cấu trúc Dự án & Tổ chức Module

- **Mã nguồn (`src/`):** Nơi chứa toàn bộ source code.
  - `src/cli`: Các file kết nối CLI.
  - `src/commands`: Logic các câu lệnh commands.
  - `src/provider-web.ts`: Nhà cung cấp dịch vụ web.
  - `src/infra`: Cơ sở hạ tầng.
  - `src/media`: Pipeline xử lý media.
- **Tests:** Các file test (`*.test.ts`) được đặt ngay cạnh file code tương ứng (colocated).
- **Tài liệu (`docs/`):** Chứa ảnh, tài liệu về hàng đợi (queue), cấu hình Pi. File build ra sẽ nằm trong `dist/`.
- **Plugins/Extensions:**
  - Nằm trong thư mục `extensions/*` (được quản lý như các gói workspace).
  - **Lưu ý quan trọng:** Chỉ thêm dependencies vào file `package.json` của extension đó, KHÔNG thêm vào `package.json` gốc của dự án trừ khi phần core thực sự cần dùng.
  - **Cài đặt:** Khi chạy install plugin, hệ thống sẽ chạy `npm install --omit=dev`. Do đó, các dependency cần thiết khi chạy (runtime) phải nằm trong `dependencies`.
  - Tránh dùng `workspace:*` trong `dependencies` vì sẽ gây lỗi khi `npm install`. Thay vào đó, hãy để `moltbot` trong `devDependencies` hoặc `peerDependencies`. Runtime sẽ tự động giải quyết `clawdbot/plugin-sdk` thông qua jiti alias.
- **Trình cài đặt (Installers):** Các file script cài đặt (`install.sh`, `install.ps1`...) nằm ở repo anh em `../molt.bot`.
- **Kênh nhắn tin (Channels):**
  - Khi sửa logic chung (routing, allowlists, pairing...), hãy nhớ kiểm tra ảnh hưởng đến **tất cả** các kênh (cả built-in và extensions).
  - Tài liệu kênh: `docs/channels/`
  - Code kênh core: `src/telegram`, `src/discord`, `src/slack`, v.v.
  - Extensions: `extensions/msteams`, `extensions/zalo`...

## Quy chuẩn Liên kết Tài liệu (Mintlify)

- **Website Docs:** [docs.molt.bot](https://docs.molt.bot).
- **Link nội bộ (trong thư mục `docs/`):** Sử dụng đường dẫn tương đối gốc (root-relative), KHÔNG có đuôi `.md`.
  - *Ví dụ đúng:* `[Cấu hình](/configuration)`
  - *Ví dụ sai:* `[Cấu hình](../configuration.md)`
- **Tham chiếu chéo (Anchor links):** Dùng anchor trên đường dẫn gốc. Ví dụ: `[Hooks](/configuration#hooks)`.
- **Tiêu đề:** Tránh dùng dấu gạch ngang dài (em dashes `—`) hoặc dấu nháy đơn `'` trong tiêu đề bài viết vì chúng làm hỏng cơ chế tạo link anchor của Mintlify.
- **Gửi link cho người khác:** Luôn dùng URL đầy đủ `https://docs.molt.bot/...`.
- **Trong README:** Luôn dùng link tuyệt đối để bấm được ngay trên GitHub.
- **Nội dung:** Viết chung chung, tránh lộ tên thiết bị/hostname cá nhân. Dùng `user@gateway-host` thay vì `hieu@may-cua-toi`.

## Vận hành VM (Dành cho nội bộ exe.dev)

- **Truy cập:** `ssh exe.dev` -> `ssh vm-name`.
- **Lưu ý:** SSH có thể chập chờn, nên dùng Shelley (web agent) hoặc giữ phiên `tmux` nếu chạy tác vụ lâu.
- **Cập nhật:** `sudo npm i -g moltbot@latest` (Cần quyền root vì cài global).
- **Cấu hình:** Dùng `moltbot config set ...` và đảm bảo `gateway.mode=local`.
- **Discord:** Lưu token thô, không cần tiền tố `DISCORD_BOT_TOKEN=`.
- **Khởi động lại (Restart):** Kill process cũ và chạy lại nohup.
- **Kiểm tra:** Dùng `moltbot channels status --probe` hoặc `tail` log.

## Lệnh Build, Test & Dev

- **Runtime:** Node **22+**. (Dự án vẫn hỗ trợ cả Node và Bun).
- **Cài đặt:** `pnpm install` (Ưu tiên). `bun install` cũng được hỗ trợ (nhớ đồng bộ `pnpm-lock.yaml`).
- **Dev:**
  - Chạy script/test: Dùng `bun` cho nhanh (`bun <file.ts>`).
  - Chạy CLI dev: `pnpm moltbot ...` (chạy qua bun/tsx) hoặc `pnpm dev`.
  - Chạy bản build (production): Dùng Node để chạy file trong `dist/`.
- **Check code:** `pnpm build` (tsc), `pnpm lint` (oxlint), `pnpm format` (oxfmt).
- **Test:** `pnpm test` (vitest).

## Phong cách Code (Coding Style)

- **Ngôn ngữ:** TypeScript (ESM). Bắt buộc dùng kiểu dữ liệu chặt chẽ (strict typing), hạn chế tối đa `any`.
- **Lint/Format:** Phải chạy `pnpm lint` trước khi commit.
- **Comment:** Viết chú thích ngắn gọn cho các đoạn logic "ảo diệu" hoặc khó hiểu.
- **Kích thước file:** Cố gắng giữ dưới ~700 dòng code. Tách nhỏ ra nếu file quá dài để dễ đọc và dễ test.
- **Đặt tên:**
  - **Moltbot**: Dùng cho tên sản phẩm, tiêu đề tài liệu.
  - `moltbot`: Dùng cho lệnh CLI, tên gói, đường dẫn file, key cấu hình.

## Kênh phát hành (Release Channels)

- **stable**: Chỉ dành cho bản release có gắn thẻ (`vYYYY.M.D`).
- **beta**: Bản thử nghiệm (`-beta.N`), có thể không có app macOS đi kèm.
- **dev**: Nhánh `main` đang phát triển.

## Hướng dẫn Test

- **Framework:** Vitest.
- **Ngưỡng coverage:** 70% (dòng, nhánh, hàm).
- **Tên file:** `*.test.ts` (unit test) và `*.e2e.test.ts` (end-to-end test).
- **Workers:** Tối đa 16 workers.
- **Live Test:** Test với key thật (API thật) dùng lệnh `CLAWDBOT_LIVE_TEST=1 pnpm test:live`.
- **Mobile:** Ưu tiên test trên thiết bị thật (iOS/Android) trước khi dùng giả lập.

## Quy trình Commit & PR

- **Tạo commit:** Dùng script `scripts/committer "<msg>" <file...>` thay vì `git commit` thủ công để đảm bảo quy chuẩn.
- **Thông điệp:** Ngắn gọn, bắt đầu bằng động từ (Ví dụ: `CLI: add verbose flag`).
- **PR:**
  - Mỗi PR nên tập trung vào một vấn đề. Đừng gom nhiều refactor không liên quan vào một PR.
  - **Review:** Dùng `gh pr view` hoặc `gh pr diff`. Đừng switch nhánh lung tung.
  - **Merge:** Ưu tiên **Rebase** để lịch sử đẹp. Nếu lịch sử quá rối rắm thì **Squash**.
  - Luôn thêm người đóng góp (PR author) vào danh sách co-contributor nếu squash.
  - Sau khi merge PR của người mới: Nhớ chạy script cập nhật danh sách contributors trong README.

## An toàn Đa Tác nhân (Multi-Agent Safety) 🤖

Khi làm việc trong môi trường có nhiều Agent cùng hoạt động:
1.  **Git Stash:** KHÔNG BAO GIỜ tự ý `git stash` hoặc `git pull --rebase --autostash` trừ khi được user yêu cầu. Agent khác có thể đang code dở.
2.  **Git Worktree:** KHÔNG tạo, xóa, sửa worktree nếu không được bảo.
3.  **Chuyển nhánh:** KHÔNG tự ý switch nhánh.
4.  **File lạ:** Nếu thấy file lạ (do agent khác tạo), cứ lờ đi và tập trung vào file của mình.
5.  **Sung đột:** Khi user bảo "push", có thể `git pull --rebase`. Khi "commit", chỉ commit file bạn sửa.

---

> **Mẹo nhỏ:** Moltbot được thiết kế rất linh hoạt. Hãy đọc kỹ code trước khi sửa, và luôn ưu tiên sự ổn định (stability) lên hàng đầu. Chúc bạn code vui vẻ! 🦞
