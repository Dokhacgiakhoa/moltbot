---
summary: "Vận hành Moltbot với Ollama (Trình chạy mô hình ngôn ngữ lớn tại chỗ)"
read_when:
  - Bạn muốn chạy Moltbot với các mô hình AI cục bộ không tốn phí qua Ollama
---
# Ollama

Ollama là một trình chạy AI cục bộ giúp bạn dễ dàng sử dụng các mô hình mã nguồn mở ngay trên máy tính của mình. Moltbot tích hợp sâu với Ollama và có thể **tự động khám phá các mô hình có khả năng sử dụng công cụ (tool-capable)** khi bạn cung cấp một khóa API bất kỳ (Ví dụ: `ollama-local`).

## Khởi động nhanh
1. **Cài đặt Ollama**: Truy cập [ollama.ai](https://ollama.ai) để tải về.
2. **Tải mô hình**:
   ```bash
   ollama pull llama3.3
   # hoặc các mô hình khác như qwen2.5-coder, deepseek-r1
   ```
3. **Kích hoạt trong Moltbot**:
   ```bash
   export OLLAMA_API_KEY="ollama-local"
   ```
4. **Sử dụng trong cấu hình**:
   ```json5
   {
     agents: {
       defaults: {
         model: { primary: "ollama/llama3.3" }
       }
     }
   }
   ```

## Cơ chế tự động khám phá mô hình
Khi bạn bật Ollama, Moltbot sẽ tự động quét các mô hình đang có trên máy của bạn tại địa chỉ `http://127.0.0.1:11434`.
- Bot sẽ lọc và chỉ lấy các mô hình có hỗ trợ tính năng gọi công cụ (`tools`).
- Tự động nhận diện các mô hình có khả năng suy nghĩ (`reasoning`) như DeepSeek-R1.
- Tự động thiết lập chi phí bằng **0$** vì tất cả chạy trên phần cứng của bạn.

## Các mẹo nâng cao
- **Thay đổi địa chỉ máy chủ**: Nếu Ollama chạy trên một máy tính khác trong mạng nội bộ, bạn có thể chỉ định `baseUrl` trong file cấu hình.
- **Sức mạnh suy luận**: Hãy ưu tiên các mô hình như `deepseek-r1:32b` hoặc `llama3.3` để có kết quả phản hồi tốt nhất.

## Giải quyết sự cố
- **Không tìm thấy Ollama**: Đảm bảo dịch vụ Ollama đang chạy (`ollama serve`). Bạn có thể kiểm tra bằng lệnh `moltbot models list` để xem bot đã nhận được mô hình chưa.
- **Không thấy mô hình trong danh sách**: Moltbot mặc định giấu các mô hình không hỗ trợ gọi công cụ. Nếu bạn vẫn muốn dùng, hãy khai báo mô hình đó thủ công trong file cấu hình.

---
Tài liệu liên quan: [Cấu hình AI cục bộ](../gateway/local-models.vi.md), [Lựa chọn mô hình AI](../../concepts/models.vi.md).
