---
summary: "Các kênh Stable, Beta và Dev: ý nghĩa, cách chuyển đổi và gắn thẻ"
read_when:
  - Bạn muốn chuyển đổi giữa các kênh stable/beta/dev
  - Bạn đang gắn thẻ hoặc phát hành các bản thử nghiệm
---

# Các kênh phát triển (Development channels)

Cập nhật lần cuối: 21/01/2026

Moltbot cung cấp ba kênh cập nhật:

- **stable**: npm dist-tag là `latest`.
- **beta**: npm dist-tag là `beta` (các bản build đang được kiểm thử).
- **dev**: nhánh `main` đang phát triển (git). npm dist-tag: `dev` (khi được phát hành).

Chúng tôi đẩy các bản build lên kênh **beta**, kiểm tra chúng, sau đó **nâng cấp một bản build đã được xác nhận lên thành `latest`** mà không cần thay đổi số phiên bản — dist-tags là nguồn thông tin chính xác cho việc cài đặt qua npm.

## Chuyển đổi kênh

Nếu chạy từ mã nguồn (Git checkout):

```bash
moltbot update --channel stable
moltbot update --channel beta
moltbot update --channel dev
```

- `stable`/`beta` sẽ checkout thẻ (tag) phù hợp mới nhất.
- `dev` sẽ chuyển sang nhánh `main` và rebase với nhánh thượng nguồn.

Nếu cài đặt global qua npm/pnpm:

```bash
moltbot update --channel stable
moltbot update --channel beta
moltbot update --channel dev
```

Lệnh này sẽ cập nhật thông qua dist-tag tương ứng của npm (`latest`, `beta`, `dev`).

Khi bạn chuyển kênh **một cách rõ ràng** bằng cờ `--channel`, Moltbot cũng sẽ điều chỉnh phương thức cài đặt:

- `dev` đảm bảo sử dụng git checkout (mặc định tại `~/moltbot`), cập nhật nó và cài đặt CLI global từ thư mục đó.
- `stable`/`beta` cài đặt từ npm sử dụng dist-tag phù hợp.

Mẹo: nếu bạn muốn dùng song song cả bản stable và dev, hãy giữ hai bản clone và trỏ gateway của bạn vào bản stable.

## Plugin và các kênh

Khi bạn chuyển kênh bằng lệnh `moltbot update`, Moltbot cũng sẽ đồng bộ nguồn của các plugin:

- `dev` ưu tiên các plugin đi kèm trong git checkout.
- `stable` và `beta` khôi phục các gói plugin được cài đặt qua npm.

---
Tài liệu liên quan: [Cập nhật](./updating.vi.md), [Hướng dẫn Bắt đầu](../start/getting-started.vi.md).
