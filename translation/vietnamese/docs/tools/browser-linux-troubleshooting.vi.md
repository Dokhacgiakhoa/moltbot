---
summary: "Khắc phục các lỗi khởi động Chrome/Chromium (CDP) khi điều khiển trình duyệt bằng Moltbot trên Linux"
read_when: "Việc điều khiển trình duyệt thất bại trên Linux, đặc biệt là khi dùng Chromium dạng snap"
---
# Khắc phục lỗi trình duyệt (Linux)

## Vấn đề: "Failed to start Chrome CDP on port 18800"

Bạn gặp lỗi khi Moltbot cố gắng khởi chạy trình duyệt:
```
{"error":"Error: Failed to start Chrome CDP on port 18800 for profile \"clawd\"."}
```

### Nguyên nhân gốc rễ
Trên Ubuntu và nhiều bản phân phối Linux khác, mặc định Chromium được cài đặt dưới dạng **gói snap**. Cơ chế bảo mật AppArmor của snap ngăn chặn việc Moltbot khởi tạo và giám sát tiến trình trình duyệt. Lệnh `apt install chromium` thực chất chỉ cài đặt một gói mồi để gọi snap.

## Giải pháp 1: Cài đặt Google Chrome chính thức (Khuyên dùng)
Bạn nên cài đặt gói `.deb` chính thức của Google Chrome vì nó không bị giới hạn bởi snap:

```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
sudo apt --fix-broken install -y  # nếu gặp lỗi phụ thuộc
```

Sau đó cập nhật cấu hình Moltbot (`~/.clawdbot/moltbot.json`):
```json
{
  "browser": {
    "enabled": true,
    "executablePath": "/usr/bin/google-chrome-stable",
    "headless": true,
    "noSandbox": true
  }
}
```

## Giải pháp 2: Sử dụng chế độ "Chỉ kết nối" (Attach-Only)
Nếu bạn bắt buộc phải dùng Chromium của snap, hãy để Moltbot kết nối vào một trình duyệt đã được khởi động thủ công:

1. Cập nhật cấu hình: `browser.attachOnly: true`.
2. Khởi động Chromium thủ công từ dòng lệnh với các cờ cần thiết:
```bash
chromium-browser --headless --no-sandbox --remote-debugging-port=18800 --user-data-dir=$HOME/.clawdbot/browser/clawd/user-data about:blank &
```

## Kiểm tra trình duyệt
Sử dụng lệnh `curl` để kiểm tra xem dịch vụ điều khiển trình duyệt đã sẵn sàng chưa:
```bash
curl -s http://127.0.0.1:18791/ | jq '{running, pid, chosenBrowser}'
```

---
Tài liệu liên quan: [Điều khiển trình duyệt](./browser.vi.md), [Tiện ích Chrome](./chrome-extension.vi.md).
