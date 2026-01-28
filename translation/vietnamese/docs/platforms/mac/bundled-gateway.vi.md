---
summary: "Môi trường chạy Gateway trên macOS (dịch vụ launchd bên ngoài)"
read_when:
  - Bạn đang đóng gói ứng dụng Moltbot.app
  - Bạn cần xử lý lỗi dịch vụ launchd trên máy Mac
---

# Gateway trên macOS (Dịch vụ launchd bên ngoài)

Cần lưu ý rằng Moltbot.app không còn đi kèm sẵn Node/Bun hay tệp thực thi Gateway bên trong. Ứng dụng này yêu cầu bạn cài đặt **CLI** `moltbot` độc lập và nó sẽ không khởi động Gateway như một tiến trình con trực tiếp. Thay vào đó, nó quản lý một dịch vụ `launchd` để giữ cho Gateway luôn chạy ngầm.

## Cài đặt CLI (Bắt buộc cho chế độ Cục bộ)

Bạn cần cài đặt Node 22+ trên máy Mac, sau đó cài đặt `moltbot` toàn cục:

```bash
npm install -g moltbot@latest
```

Nút **Install CLI** trong ứng dụng macOS cũng sẽ thực hiện quy trình tương tự thông qua npm hoặc pnpm.

## Launchd (Gateway chạy như một LaunchAgent)

- **Tên nhãn (Label)**: `bot.molt.gateway`.
- **Vị trí tệp cấu hình (Plist)**: `~/Library/LaunchAgents/bot.molt.gateway.plist`.

**Cơ chế hoạt động:**
- Khi bạn chuyển trạng thái "Moltbot Active", ứng dụng sẽ nạp (load) hoặc gỡ (unload) tệp cấu hình này.
- Việc thoát ứng dụng (Quit) **không** làm dừng Gateway (vì launchd sẽ giữ nó luôn chạy).
- Nếu đã có một Gateway chạy sẵn trên cổng cấu hình, ứng dụng sẽ tự động kết nối vào đó thay vì khởi động cái mới.

## Kiểm tra nhanh dịch vụ

Bạn có thể kiểm tra xem Gateway có phản hồi không bằng lệnh sau trong Terminal:

```bash
moltbot --version
moltbot gateway call health --timeout 3000
```

---
Tài liệu liên quan: [Cài đặt CLI](../../install/index.vi.md), [Vận hành Gateway](../../gateway/index.vi.md).
