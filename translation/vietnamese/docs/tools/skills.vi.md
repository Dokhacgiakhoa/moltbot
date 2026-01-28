---
summary: "Kỹ năng (Skills): quản lý vs không gian làm việc, quy tắc giới hạn và cấu hình"
read_when:
  - Thêm hoặc sửa đổi các kỹ năng
  - Thay đổi quy tắc tải hoặc giới hạn kỹ năng
---
# Kỹ năng (Skills)

Moltbot sử dụng các thư mục kỹ năng tương thích với tiêu chuẩn **[AgentSkills](https://agentskills.io)** để dạy cho agent cách sử dụng các công cụ. Mỗi kỹ năng là một thư mục chứa file `SKILL.md` bao gồm các hướng dẫn và quy tắc vận hành.

## Vị trí và Thứ tự ưu tiên (Precedence)

Kỹ năng được tải từ **ba** nơi:

1) **Kỹ năng đi kèm (Bundled)**: đi kèm với bản cài đặt Moltbot.
2) **Kỹ năng cục bộ (Managed/local)**: tại `~/.clawdbot/skills`.
3) **Kỹ năng không gian làm việc (Workspace)**: tại `<workspace>/skills`.

Nếu có sự trùng tên, thứ tự ưu tiên sẽ là:
**Workspace** (cao nhất) → **Local** → **Bundled** (thấp nhất).

## Kỹ năng riêng của Agent vs Kỹ năng dùng chung

Trong thiết lập **đa tác nhân (multi-agent)**, mỗi agent có không gian làm việc riêng:

- **Kỹ năng riêng (Per-agent skills)**: Nằm trong `<workspace>/skills` của riêng agent đó.
- **Kỹ năng dùng chung (Shared skills)**: Nằm trong `~/.clawdbot/skills`, tất cả các agent trên cùng máy đều thấy được.

## ClawdHub (Cài đặt & Đồng bộ)

ClawdHub là kho lưu trữ kỹ năng công cộng cho Moltbot tại **https://clawdhub.com**. Bạn có thể dùng nó để khám phá, cài đặt và cập nhật kỹ năng.

Các lệnh thường dùng:
- Cài đặt một kỹ năng: `clawdhub install <tên-kỹ-năng>`
- Cập nhật tất cả: `clawdhub update --all`

## Lưu ý về Bảo mật
- Hãy coi các kỹ năng từ bên thứ ba như là **mã nguồn tin cậy**. Hãy đọc kỹ hướng dẫn trước khi bật.
- Khuyên dùng chế độ sandbox khi sử dụng các công cụ rủi ro cao. Xem [Sandboxing](../gateway/sandboxing.vi.md).

## Cấu hình ghi đè (`~/.clawdbot/moltbot.json`)
Bạn có thể bật/tắt kỹ năng và cung cấp các biến môi trường (như API key) trong cấu hình:

```json5
{
  skills: {
    entries: {
      "nano-banana-pro": {
        enabled: true,
        apiKey: "MÃ_API_CỦA_BẠN"
      }
    }
  }
}
```

---
Tài liệu liên quan: [Công cụ](./index.vi.md), [Cấu hình Gateway](../gateway/configuration.vi.md).
