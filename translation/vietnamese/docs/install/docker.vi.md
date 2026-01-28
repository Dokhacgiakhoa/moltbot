---
summary: "Thiết lập và làm quen với Moltbot dựa trên Docker (tùy chọn)"
read_when:
  - Bạn muốn chạy gateway trong container thay vì cài đặt trực diện trên máy
  - Bạn đang kiểm tra luồng hoạt động với Docker
---

# Docker (Tùy chọn)

Việc sử dụng Docker là **tùy chọn**. Chỉ sử dụng nếu bạn muốn chạy gateway trong container hoặc để kiểm tra luồng hoạt động của Docker.

## Docker có phù hợp với tôi không?

- **Có**: Nếu bạn muốn một môi trường gateway cô lập, có thể xóa bỏ nhanh chóng hoặc chạy Moltbot trên máy chủ mà không muốn cài đặt các thành phần trực tiếp lên máy.
- **Không**: Nếu bạn đang chạy trên máy cá nhân và chỉ muốn tốc độ phát triển/sử dụng nhanh nhất. Hãy dùng luồng cài đặt bình thường.
- **Lưu ý về Sandboxing**: Tính năng sandbox của agent cũng sử dụng Docker, nhưng nó **không** yêu cầu toàn bộ gateway phải chạy trong Docker. Xem [Sandboxing](../gateway/sandboxing.vi.md).

Hướng dẫn này bao gồm:
- Gateway trong Container (Chạy toàn bộ Moltbot trong Docker)
- Agent Sandbox cho mỗi phiên (Gateway chạy trên máy host + các công cụ của agent cô lập trong Docker)

Chi tiết về Sandboxing: [Sandboxing](../gateway/sandboxing.vi.md)

## Yêu cầu

- Docker Desktop (hoặc Docker Engine) + Docker Compose v2
- Đủ dung lượng đĩa cho images và nhật ký (logs)

## Gateway trong Container (Docker Compose)

### Bắt đầu nhanh (Khuyên dùng)

Từ thư mục gốc của repo:

```bash
./docker-setup.sh
```

Kịch bản (script) này sẽ:
- Build image cho gateway
- Chạy trình hướng dẫn thiết lập (onboarding wizard)
- In ra các gợi ý thiết lập nhà cung cấp (provider)
- Khởi động gateway qua Docker Compose
- Tạo một gateway token và ghi vào file `.env`

Các biến môi trường tùy chọn:
- `CLAWDBOT_DOCKER_APT_PACKAGES` — cài đặt thêm các gói apt trong quá trình build
- `CLAWDBOT_EXTRA_MOUNTS` — thêm các điểm gắn (mount) từ máy host
- `CLAWDBOT_HOME_VOLUME` — lưu trữ bền vững thư mục `/home/node` trong một volume có tên

Sau khi hoàn tất:
- Mở `http://127.0.0.1:18789/` trong trình duyệt.
- Dán token vào Control UI (Settings → token).

Cấu hình và không gian làm việc sẽ được ghi trên máy host tại:
- `~/.clawdbot/`
- `~/clawd`

Chạy trên VPS? Xem [Hetzner (Docker VPS)](../platforms/hetzner.vi.md).

### Luồng thủ công (Compose)

```bash
docker build -t moltbot:local -f Dockerfile .
docker compose run --rm moltbot-cli onboard
docker compose up -d moltbot-gateway
```

### Thiết lập Kênh (Tùy chọn)

Sử dụng container CLI để cấu hình các kênh, sau đó khởi động lại gateway nếu cần.

WhatsApp (QR):
```bash
docker compose run --rm moltbot-cli channels login
```

Telegram (Bot token):
```bash
docker compose run --rm moltbot-cli channels add --channel telegram --token "<mã_token>"
```

Tài liệu: [WhatsApp](../channels/whatsapp.vi.md), [Telegram](../channels/telegram.vi.md), [Discord](../channels/discord.vi.md)

## Agent Sandbox (Gateway trên máy host + công cụ Docker)

Tìm hiểu sâu hơn: [Sandboxing](../gateway/sandboxing.vi.md)

### Cơ chế hoạt động

Khi tính năng `agents.defaults.sandbox` được bật, các **phiên làm việc không phải là main** sẽ chạy các công cụ bên trong một container Docker. Gateway vẫn nằm trên máy host của bạn, nhưng việc thực thi công cụ được cô lập.

### Bật Sandboxing

```json5
{
  agents: {
    defaults: {
      sandbox: {
        mode: "non-main", // off | non-main | all
        scope: "agent", // session | agent | shared
        workspaceAccess: "none", // none | ro | rw
        docker: {
          image: "moltbot-sandbox:bookworm-slim",
          network: "none",
          memory: "1g",
          cpus: 1
        }
      }
    }
  }
}
```

### Build image sandbox mặc định

```bash
scripts/sandbox-setup.sh
```

Lệnh này sẽ build image `moltbot-sandbox:bookworm-slim` sử dụng `Dockerfile.sandbox`.

## Khắc phục lỗi

- Thiếu Image: Build bằng [`scripts/sandbox-setup.sh`](https://github.com/moltbot/moltbot/blob/main/scripts/sandbox-setup.sh).
- Container không chạy: Nó sẽ tự động tạo theo yêu cầu cho mỗi phiên làm việc.
- Lỗi phân quyền trong sandbox: Thiết lập `docker.user` thành UID:GID khớp với quyền sở hữu không gian làm việc của bạn.
