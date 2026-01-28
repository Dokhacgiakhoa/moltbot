---
summary: "Cách sử dụng các mô hình Amazon Bedrock (Converse API) với Moltbot"
---
# Amazon Bedrock

Moltbot có thể sử dụng các mô hình **Amazon Bedrock** thông qua trình cung cấp truyền phát (streaming) **Bedrock Converse**. Việc xác thực của Bedrock sử dụng chuỗi thông tin xác thực mặc định của **AWS SDK**, thay vì sử dụng API key.

## Các thông số hỗ trợ

- **Nhà cung cấp**: `amazon-bedrock`
- **API**: `bedrock-converse-stream`
- **Xác thực**: Thông tin AWS (biến môi trường, tệp cấu hình chung hoặc vai trò thực thể - instance role)
- **Vùng (Region)**: `AWS_REGION` hoặc `AWS_DEFAULT_REGION` (mặc định: `us-east-1`)

## Tự động khám phá mô hình

Nếu phát hiện thông tin xác thực AWS, Moltbot có thể tự động tìm kiếm các mô hình Bedrock hỗ trợ **truyền phát** và **đầu ra văn bản**. Kết quả khám phá được lưu tạm (cache) trong vòng 1 giờ.

Cấu hình tùy chọn nằm tại `models.bedrockDiscovery`:

```json
{
  "models": {
    "bedrockDiscovery": {
      "enabled": true,
      "region": "us-east-1",
      "providerFilter": ["anthropic", "amazon"]
    }
  }
}
```

## Thiết lập thủ công

1.  Đảm bảo thông tin xác thực AWS có sẵn trên **máy chủ Gateway**:

```bash
export AWS_ACCESS_KEY_ID="AKIA..."
export AWS_SECRET_ACCESS_KEY="..."
export AWS_REGION="us-east-1"
```

2.  Thêm nhà cung cấp và mô hình Bedrock vào cấu hình của bạn:

```json
{
  "models": {
    "providers": {
      "amazon-bedrock": {
        "baseUrl": "https://bedrock-runtime.us-east-1.amazonaws.com",
        "api": "bedrock-converse-stream",
        "auth": "aws-sdk",
        "models": [
          {
            "id": "anthropic.claude-opus-4-5-20251101-v1:0",
            "name": "Claude Opus 4.5 (Bedrock)",
            "input": ["text", "image"]
          }
        ]
      }
    }
  }
}
```

## Vai trò thực thể EC2 (Instance Roles)

Khi chạy Moltbot trên thực thể EC2 đã gắn vai trò IAM, AWS SDK sẽ tự động sử dụng dịch vụ thông tin thực thể (IMDS) để xác thực.

**Mẹo nhỏ**: Hãy đặt `AWS_PROFILE=default` để báo hiệu rằng thông tin xác thực AWS đã có sẵn.

**Các quyền IAM cần thiết**:
- `bedrock:InvokeModel`
- `bedrock:InvokeModelWithResponseStream`
- `bedrock:ListFoundationModels` (dùng cho việc tự động khám phá)

Hoặc gắn chính sách quản lý `AmazonBedrockFullAccess`.

## Lưu ý

- Bạn cần bật quyền **truy cập mô hình** (model access) trong tài khoản/vùng AWS của mình.
- Khám phá mô hình tự động yêu cầu quyền `bedrock:ListFoundationModels`.
- Nếu bạn có nhiều hồ sơ (profiles), hãy đặt `AWS_PROFILE` trên máy chủ Gateway.

---
Tài liệu liên quan: [Cấu hình hệ thống](./gateway/configuration.vi.md), [Nhà cung cấp AI](./providers/index.vi.md).
