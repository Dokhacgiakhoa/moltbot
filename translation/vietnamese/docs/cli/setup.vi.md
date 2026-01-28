---
summary: "Tài liệu tham khảo lệnh `moltbot setup` (Khởi tạo cấu hình + không gian làm việc)"
read_when:
  - Bạn muốn khởi tạo hệ thống lần đầu mà không dùng thuật sĩ đầy đủ
  - Bạn muốn đặt đường dẫn mặc định cho không gian làm việc của Agent
---

# `moltbot setup`

Lệnh này dùng để khởi tạo file cấu hình tại `~/.clawdbot/moltbot.json` và chuẩn bị không gian làm việc cho Agent.

Tài liệu liên quan:
- Bắt đầu nhanh: [Bắt đầu nhanh](../../start/getting-started.vi.md)
- Thuật sĩ: [Onboarding](../../start/onboarding.vi.md)

## Ví dụ sử dụng

```bash
moltbot setup
moltbot setup --workspace ~/my-agent-folder
```

Nếu bạn muốn chạy đồng thời cả trình thuật sĩ thông qua lệnh setup:

```bash
moltbot setup --wizard
```
