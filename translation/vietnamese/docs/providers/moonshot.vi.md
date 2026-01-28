---
summary: "Cấu hình Moonshot K2 và Kimi Code (nhà cung cấp và mã khóa riêng biệt)"
read_when:
  - Bạn muốn sử dụng mô hình Kimi từ Moonshot AI trong Moltbot
---
# Moonshot AI (Kimi)

Moonshot AI cung cấp các mô hình **Kimi** mạnh mẽ thông qua API tương thích với chuẩn OpenAI. Moltbot hỗ trợ cả nền tảng mở Moonshot (K2) và phiên bản tối ưu cho lập trình Kimi Code.

## Danh sách các phiên bản Kimi K2:
- `kimi-k2.5` (Mô hình mới nhất)
- `kimi-k2-turbo`
- `kimi-k2-thinking` (Mô hình hỗ trợ khả năng suy nghĩ sâu)

## Thiết lập nhanh qua CLI:
Đối với Moonshot API:
```bash
moltbot onboard --auth-choice moonshot-api-key
```

Đối với Kimi Code:
```bash
moltbot onboard --auth-choice kimi-code-api-key
```

**Lưu ý quan trọng**: Moonshot và Kimi Code là hai nền tảng riêng biệt. Mã API key của chúng không dùng chung được cho nhau và địa chỉ kết nối (endpoint) cũng khác nhau.

## Ví dụ cấu hình trong file `moltbot.json`:
```json5
{
  env: { MOONSHOT_API_KEY: "sk-..." },
  agents: {
    defaults: {
      model: { primary: "moonshot/kimi-k2.5" }
    }
  }
}
```

## Giải quyết sự cố
- **Địa chỉ kết nối**: Nếu bạn đang ở Trung Quốc và gặp vấn đề kết nối, hãy thử đổi `baseUrl` thành `https://api.moonshot.cn/v1`.
- **Mô hình lập trình**: Kimi Code (`kimi-for-coding`) có khả năng xử lý các đoạn mã phức tạp rất tốt với cửa sổ ngữ cảnh lên tới 262k tokens.

---
Tài liệu liên quan: [Tất cả nhà cung cấp](./index.vi.md), [Khắc phục sự cố](../gateway/troubleshooting.vi.md).
