---
summary: "Định tuyến đa Agent: Các Agent cô lập, tài khoản kênh và ghép nối"
title: Định tuyến đa Agent
read_when: "Bạn muốn chạy nhiều Agent độc lập (khác không gian làm việc và xác thực) trong cùng một tiến trình Gateway."
---

# Định tuyến đa Agent

Mục tiêu: Chạy nhiều Agent **cô lập** (tách biệt về không gian làm việc, cấu hình và phiên làm việc), cùng với nhiều tài khoản của các kênh nhắn tin (ví dụ: hai tài khoản WhatsApp) trong một dịch vụ Gateway duy nhất. Các tin nhắn đến sẽ được định tuyến tới từng Agent thông qua quy tắc ghép nối (bindings).

## "Một Agent" nghĩa là gì?

Một **Agent** là một "bộ não" hoàn chỉnh được giới hạn trong:

- **Không gian làm việc (Workspace)**: Các tệp chỉ dẫn (`AGENTS.md`, `SOUL.md`, `USER.md`), ghi chú cục bộ và các quy tắc tính cách.
- **Thư mục trạng thái (`agentDir`)**: Lưu giữ hồ sơ xác thực, danh mục mô hình và cấu hình riêng.
- **Kho lưu trữ phiên**: Lịch sử chat và trạng thái định tuyến.

Thông tin xác thực (Auth profiles) là **riêng cho từng Agent**. Mỗi Agent chỉ đọc từ thư mục của chính nó. Không bao giờ dùng chung thư mục `agentDir` giữa các Agent vì sẽ gây ra xung đột về dữ liệu.

Gateway có thể host **một Agent** (mặc định) hoặc **nhiều Agent** chạy song song.

## Các đường dẫn chính

- Cấu hình chung: `~/.clawdbot/moltbot.json`
- Thư mục trạng thái: `~/.clawdbot`
- Không gian làm việc: `~/clawd-<agentId>`
- Kho lưu trữ phiên: `~/.clawdbot/agents/<agentId>/sessions`

## Thuật sĩ thêm Agent

Sử dụng lệnh sau để thêm một Agent cô lập mới:

```bash
moltbot agents add <tên-agent>
```

Sau đó thêm quy tắc định tuyến (`bindings`) để dẫn các tin nhắn đến đúng nơi. Kiểm tra danh sách bằng lệnh:

```bash
moltbot agents list --bindings
```

## Nhiều Agent = Nhiều người dùng, Nhiều tính cách

Với thiết lập đa Agent, mỗi `agentId` trở thành một **nhân vật hoàn toàn độc lập**:

- **Sử dụng số điện thoại/tài khoản khác nhau**.
- **Tính cách khác nhau** (quy định trong tệp `SOUL.md` riêng).
- **Bộ nhớ tách biệt** (không bị lẫn dữ liệu giữa các người dùng).

Điều này cho phép **nhiều người** dùng chung một máy chủ Gateway nhưng vẫn giữ cho bộ não AI và dữ liệu cá nhân của mình được bảo mật tuyệt đối.

## Định tuyến thông minh

Moltbot chọn Agent cho mỗi tin nhắn dựa theo quy tắc **"Khớp chính xác nhất sẽ thắng"**:

1. Khớp theo ID người dùng/nhóm cụ thể (`peer`).
2. Khớp theo máy chủ (Discord/Slack).
3. Khớp theo ID tài khoản của kênh.
4. Ưu tiên cuối cùng là Agent mặc định (`main`).

## Ví dụ: Hai WhatsApp cho hai Agent khác nhau

```json
{
  "agents": {
    "list": [
      { "id": "alex", "workspace": "~/clawd-alex" },
      { "id": "mia", "workspace": "~/clawd-mia" }
    ]
  },
  "bindings": [
    { "agentId": "alex", "match": { "channel": "whatsapp", "accountId": "personal" } },
    { "agentId": "mia", "match": { "channel": "whatsapp", "accountId": "work" } }
  ]
}
```

Trong ví dụ này, tin nhắn từ tài khoản WhatsApp cá nhân sẽ do Agent Alex trả lời, còn tin nhắn từ tài khoản công việc sẽ do Mia xử lý.

---
Tài liệu liên quan: [Cấu hình Sandbox & Công cụ đa Agent](../multi-agent-sandbox-tools.vi.md), [Nhóm phát tin](../broadcast-groups.vi.md).
