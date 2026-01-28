---
summary: "Sử dụng Anthropic Claude qua API key hoặc setup-token trong Moltbot"
read_when:
  - Bạn muốn dùng các model Claude của Anthropic trong Moltbot
---
# Anthropic (Claude)

Anthropic là nhà phát triển dòng mô hình **Claude** nổi tiếng. Moltbot hỗ trợ kết nối với Anthropic thông qua hai hình thức: Sử dụng mã API key truyền thống hoặc sử dụng **setup-token**.

## Lựa chọn A: Sử dụng Anthropic API key
**Phù hợp nhất cho**: Người dùng muốn dùng API chuẩn và trả phí theo lưu lượng sử dụng.
Bạn có thể tạo mã API key này trong trang quản trị Anthropic Console.

### Thiết lập qua CLI:
```bash
moltbot onboard
# Chọn: Anthropic API key
```

### Cấu hình trong file:
```json5
{
  env: { ANTHROPIC_API_KEY: "sk-ant-..." },
  agents: { defaults: { model: { primary: "anthropic/claude-opus-4-5" } } }
}
```

## Lựa chọn B: Sử dụng Claude setup-token
**Phù hợp nhất cho**: Người dùng đã có gói đăng ký trả phí (Subscription) của Claude và muốn sử dụng trong Moltbot.

### Cách lấy setup-token:
Mã setup-token được tạo bởi công cụ **Claude Code CLI** (do Anthropic cung cấp). Bạn có thể chạy lệnh này trên bất kỳ máy tính nào:
```bash
claude setup-token
```
Sau đó, dán mã này vào Moltbot khi được hỏi trong quá trình `onboard`.

## Ghi nhớ về bộ nhớ tạm (Prompt Caching)
Moltbot hỗ trợ tính năng bộ nhớ tạm của Anthropic để giúp giảm chi phí và tăng tốc độ phản hồi. Bạn có thể điều chỉnh thời gian lưu tạm (TTL) trong phần cấu hình của model.

## Giải quyết sự cố
- **Lỗi 401 / Token hết hạn**: Nếu bạn dùng gói Subscription, Token có thể bị thu hồi. Hãy chạy lại lệnh `claude setup-token` để lấy mã mới.
- **Không tìm thấy API key cho nhà cung cấp "anthropic"**: Hãy nhớ rằng mỗi Agent có thể có bộ mã xác thực riêng. Nếu bạn tạo Agent mới, hãy đảm bảo đã cấp quyền truy cập cho Agent đó.

---
Tài liệu liên quan: [Cấu hình Gateway](../gateway/configuration.vi.md), [Khái niệm mô hình AI](../../concepts/models.vi.md).
