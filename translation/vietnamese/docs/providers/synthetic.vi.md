---
summary: "Sử dụng API tương thích Anthropic của Synthetic trong Moltbot"
read_when:
  - Bạn muốn dùng Synthetic làm nhà cung cấp mô hình cho bot của mình
---
# Synthetic

Synthetic cung cấp các điểm kết nối (endpoints) tương thích hoàn toàn với chuẩn của Anthropic. Moltbot nhận diện đây là nhà cung cấp `synthetic` và sử dụng bộ API tin nhắn của Anthropic để giao tiếp.

## Thiết lập nhanh
1. **Lấy mã khóa**: Lấy mã `SYNTHETIC_API_KEY` từ tài khoản Synthetic của bạn.
2. **Chạy quy trình thiết lập**:
   ```bash
   moltbot onboard --auth-choice synthetic-api-key
   ```

## Mô hình mặc định
Moltbot thường sử dụng MiniMax M2.1 làm mô hình mặc định cho nhà cung cấp này:
`synthetic/hf:MiniMaxAI/MiniMax-M2.1`

## Danh mục các mô hình phổ biến trên Synthetic:
Synthetic hỗ trợ rất nhiều mô hình từ các nhà phát triển khác nhau được lưu trữ trên HuggingFace (hf):
- **MiniMax M2.1**: `hf:MiniMaxAI/MiniMax-M2.1`
- **DeepSeek V3**: `hf:deepseek-ai/DeepSeek-V3`
- **Llama 3.3**: `hf:meta-llama/Llama-3.3-70B-Instruct`
- **Qwen 3 Coder**: `hf:Qwen/Qwen3-Coder-480B-A35B-Instruct`

## Ghi chú quan trọng
- Các model trên Synthetic thường được thiết lập chi phí bằng 0 trong cấu hình mặc định (tùy vào gói cước của bạn).
- Nếu bạn có danh sách giới hạn mô hình (allowlist), hãy nhớ thêm tất cả các model bạn định dùng từ Synthetic vào danh sách đó.

---
Tài liệu liên quan: [Cấu hình hệ thống](../gateway/configuration.vi.md), [Mô hình AI](../../concepts/models.vi.md).
