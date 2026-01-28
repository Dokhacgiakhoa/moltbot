---
summary: "Chạy Moltbot với các mô hình AI cục bộ (LM Studio, vLLM, LiteLLM)"
read_when:
  - Bạn muốn chạy AI ngay trên phần cứng của mình để đảm bảo quyền riêng tư tuyệt đối
  - Bạn sở hữu dàn máy có GPU mạnh
---

# Mô hình AI chạy cục bộ (Local models)

Việc chạy AI cục bộ là hoàn toàn khả thi, tuy nhiên Moltbot yêu cầu một cửa sổ ngữ cảnh (Context Window) lớn và khả năng phòng vệ mạnh mẽ trước các yêu cầu xấu. Một dàn máy GPU mạnh (như Mac Studio tối tân hoặc dàn GPU chuyên dụng) là điều kiện lý tưởng. Một GPU **24 GB** đơn lẻ chỉ có thể xử lý các câu lệnh ngắn với độ trễ cao.

## Lựa chọn khuyên dùng: LM Studio + MiniMax M2.1

Đây là tổ hợp tốt nhất hiện nay để chạy AI ngay trên máy tính của bạn:
1. Tải và cài đặt [LM Studio](https://lmstudio.ai).
2. Tải mô hình **MiniMax M2.1** (phiên bản đầy đủ nhất mà máy bạn có thể chịu tải).
3. Bật chế độ "Local Server" trong LM Studio (mặc định tại cổng `1234`).
4. Cấu hình Moltbot để trỏ về địa chỉ này.

**Ví dụ cấu hình:**
```json5
{
  "agents": {
    "defaults": {
      "model": { "primary": "lmstudio/minimax-m2.1" }
    }
  },
  "models": {
    "providers": {
      "lmstudio": {
        "baseUrl": "http://127.0.0.1:1234/v1",
        "apiKey": "lmstudio",
        "api": "openai-responses", // Dùng chuẩn OpenAI
        "models": [
          {
            "id": "minimax-m2.1",
            "name": "MiniMax M2.1 Local",
            "contextWindow": 196608
          }
        ]
      }
    }
  }
}
```

## Mô hình kết hợp (Hybrid)
Bạn có thể cấu hình để Agent dùng mô hình cục bộ làm mặc định, nhưng vẫn giữ các mô hình đám mây (như Claude Opus) làm phương án dự phòng khi máy chủ tại nhà của bạn bị tắt hoặc quá tải.

## Lưu ý về bảo mật
Các mô hình chạy cục bộ thường thiếu các bộ lọc nội dung (safety filters) của các nhà cung cấp lớn. Vì vậy, hãy cẩn trọng khi cho phép người lạ truy cập vào Bot chạy cục bộ của bạn để tránh các rủi ro về mã độc hoặc lệnh thực thi nguy hiểm.

---
Tài liệu liên quan: [Cấu hình mô hình](../concepts/models.vi.md), [Nhà cung cấp AI](../concepts/model-providers.vi.md).
