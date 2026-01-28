---
summary: "Không gian làm việc của Agent: Vị trí, sơ đồ thư mục và chiến lược sao lưu"
read_when:
  - Bạn muốn tìm hiểu về thư mục làm việc của Agent hoặc cấu trúc tệp tin
  - Bạn muốn sao lưu hoặc di chuyển không gian làm việc sang máy tính khác
---

# Không gian làm việc (Workspace)

Không gian làm việc là "nhà" của Agent. Đây là thư mục làm việc duy nhất dành cho các công cụ tệp tin và ngữ cảnh của Agent. Hãy giữ nó riêng tư và coi nó như bộ nhớ của Agent.

Thư mục này tách biệt hoàn toàn với `~/.clawdbot/` (nơi lưu trữ cấu hình, thông tin xác thực và lịch sử các phiên làm việc).

**Quan trọng:** Không gian làm việc là thư mục làm việc mặc định (`cwd`), không phải là một môi trường bị khóa (sandbox) hoàn toàn. Các công cụ sẽ giải quyết các đường dẫn tương đối dựa trên thư mục này, nhưng các đường dẫn tuyệt đối vẫn có thể truy cập các nơi khác trên máy tính của bạn trừ khi bạn bật tính năng [Sandbox](../gateway/sandboxing.md).

## Vị trí mặc định

- Mặc định: `~/clawd`
- Nếu bạn thiết lập `CLAWDBOT_PROFILE` khác mặc định, vị trí sẽ là `~/clawd-<tên-profile>`.
- Bạn có thể ghi đè trong tệp `moltbot.json`:

```json
{
  "agent": {
    "workspace": "~/clawd"
  }
}
```

## Bản đồ các tệp tin trong không gian làm việc

Đây là các tệp tiêu chuẩn mà Moltbot mong đợi có bên trong không gian làm việc:

- **`AGENTS.md`**: Chỉ dẫn vận hành cho Agent và cách nó nên sử dụng bộ nhớ. Thường chứa các quy tắc, mức độ ưu tiên và cách cư xử.
- **`SOUL.md`**: Định nghĩa tính cách, giọng văn và các giới hạn đạo đức/hành vi.
- **`USER.md`**: Thông tin về người dùng (là bạn) và cách Agent nên xưng hô.
- **`IDENTITY.md`**: Tên của Agent, phong cách và biểu tượng đại diện. Thường được tạo trong lần chạy đầu tiên.
- **`TOOLS.md`**: Các ghi chú về công cụ cục bộ của bạn. Đây chỉ là tài liệu hướng dẫn cho Agent, không dùng để bật/tắt công cụ.
- **`HEARTBEAT.md`**: (Tùy chọn) Danh sách kiểm tra ngắn gọn cho các lượt chạy tự động (heartbeat).
- **`BOOTSTRAP.md`**: Quy trình cho lần đầu tiên sử dụng. Sẽ biến mất sau khi hoàn thành.
- **`memory/YYYY-MM-DD.md`**: Nhật ký bộ nhớ hàng ngày. Khuyên dùng Agent nên đọc dữ liệu hôm nay và hôm qua khi bắt đầu phiên mới.

Chi tiết về bộ nhớ: [Bộ nhớ Agent](./memory.vi.md).

## Những gì KHÔNG nằm trong không gian làm việc

Các thành phần sau nằm trong `~/.clawdbot/` và **KHÔNG** nên được đưa vào kho lưu trữ (Git) của không gian làm việc:
- Cấu hình Gateway (`moltbot.json`).
- Thông tin xác thực (token, mã API).
- Lịch sử trò chuyện của các phiên làm việc.

## Sao lưu bằng Git (Khuyên dùng, chế độ Riêng tư)

Hãy coi không gian làm việc là bộ não riêng tư của bạn. Bạn nên đưa nó vào một kho lưu trữ Git **bí mật (private)** để có thể khôi phục khi cần.

### 1) Khởi tạo kho lưu trữ
```bash
cd ~/clawd
git init
git add .
git commit -m "Khởi tạo không gian làm việc Agent"
```

### 2) Thêm máy chủ lưu trữ (Ví dụ: GitHub)
1. Tạo một repository mới trên GitHub ở chế độ **Private**.
2. Thêm địa chỉ và đẩy dữ liệu lên:
```bash
git remote add origin <địa-chỉ-github-cua-ban>
git push -u origin main
```

**LƯU Ý QUAN TRỌNG:** Đừng bao giờ lưu mật khẩu hay mã API vào các tệp tin trong không gian làm việc, dù kho lưu trữ của bạn là riêng tư.

---
Tài liệu liên quan: [Cấu hình Gateway](../gateway/configuration.vi.md), [Định tuyến kênh](./channel-routing.vi.md).
