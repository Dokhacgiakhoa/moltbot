---
summary: "Hệ thống bổ trợ qua CLI: Sử dụng các AI chạy cục bộ làm phương án dự phòng"
read_when:
  - Bạn muốn có một phương án dự phòng khi các nhà cung cấp API (như Claude/OpenAI) gặp sự cố
  - Bạn đang chạy AI ngay trên máy tính của mình và muốn Moltbot tận dụng nó
---

# Hệ thống bổ trợ qua CLI (CLI Backends)

Moltbot có thể gọi các **công cụ dòng lệnh AI cục bộ** để làm **phương án dự phòng (fallback)** khi các dịch vụ API đám mây bị lỗi, bị giới hạn băng thông hoặc gặp sự cố tạm thời. Đây là một cơ chế an toàn với các đặc điểm:

- **Các công cụ bị tắt**: Chỉ xử lý văn bản thuần, không thể thực thi lệnh hệ thống.
- **Tính ổn định cao**: Phản hồi văn bản đáng tin cậy vì chạy ngay trên máy của bạn.
- **Hỗ trợ phiên làm việc**: Agent vẫn nhớ ngữ cảnh của các câu hỏi trước đó.
- **Có thể xử lý hình ảnh**: Nếu công cụ CLI đó hỗ trợ nạp đường dẫn ảnh.

Đây được coi là **"mạng lưới an toàn"** giúp Agent luôn có thể trả lời bạn ngay cả khi mất kết nối mạng quốc tế hoặc hết tiền trong tài khoản AI đám mây.

## Bắt đầu nhanh (Không cần cấu hình)

Bạn có thể dùng Claude Code CLI hoặc Codex CLI ngay lập tức (Moltbot đã tích hợp sẵn các cài đặt mặc định):

```bash
moltbot agent --message "Xin chào" --model claude-cli/opus
```

Nếu bạn đã cài đặt `claude` hoặc `codex` trên máy, lệnh trên sẽ tự động hoạt động mà không cần thêm bất kỳ khóa API nào trong cấu hình Moltbot.

## Sử dụng làm phương án dự phòng

Bạn nên thêm một CLI Backend vào danh sách `fallbacks` trong file cấu hình để hệ thống tự động chuyển sang khi mô hình chính gặp lỗi:

```json
{
  "agents": {
    "defaults": {
      "model": {
        "primary": "anthropic/claude-3-5-sonnet",
        "fallbacks": ["claude-cli/opus"]
      }
    }
  }
}
```

## Các hạn chế

- **Không hỗ trợ công cụ (Tools)**: Backend qua CLI không nhận được các yêu cầu gọi công cụ của Moltbot. Tuy nhiên, bản thân công cụ CLI đó có thể vẫn chạy được các kỹ năng riêng của nó.
- **Không hỗ trợ truyền tin (Streaming)**: Kết quả gửi về một lần thay vì hiện ra từng chữ một.
- **Phụ thuộc vào cấu hình CLI**: Nếu bạn chưa đăng nhập hoặc chưa cấu hình đúng công cụ CLI ở bên ngoài, Moltbot cũng sẽ không gọi được nó.

---
Tài liệu liên quan: [Dự phòng lỗi mô hình](../concepts/model-failover.vi.md), [Nhà cung cấp mô hình](../concepts/model-providers.vi.md).
