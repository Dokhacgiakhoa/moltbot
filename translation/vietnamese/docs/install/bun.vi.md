---
summary: "Quy trình làm việc với Bun (thử nghiệm): Cách cài đặt và những lưu ý so với pnpm"
read_when:
  - Bạn muốn tốc độ phát triển trên máy cục bộ nhanh nhất (bun + watch)
  - Bạn gặp lỗi với các kịch bản cài đặt (lifecycle scripts) của Bun
---

# Bun (thử nghiệm)

Mục tiêu: chạy kho lưu trữ này với **Bun** (tùy chọn, không khuyến khích cho WhatsApp/Telegram) mà không làm thay đổi quy trình làm việc chuẩn của pnpm.

⚠️ **Không khuyến nghị dùng cho Gateway khi chạy thực tế** (Có thể gặp lỗi với WhatsApp/Telegram). Hãy sử dụng Node cho môi trường sản xuất.

## Trạng thái hỗ trợ
- Bun là một môi trường chạy máy cục bộ tùy chọn để thực thi trực tiếp các tệp TypeScript (`bun run …`, `bun --watch …`).
- `pnpm` vẫn là công cụ mặc định để đóng gói (build) và được hỗ trợ đầy đủ nhất.
- Bun không sử dụng tệp `pnpm-lock.yaml` và sẽ bỏ qua nó.

## Cài đặt
Mặc định:
```sh
bun install
```
Lưu ý: Các tệp khóa của Bun (`bun.lock`/`bun.lockb`) đã được cấu hình để Git bỏ qua. Nếu bạn không muốn tạo file khóa:
```sh
bun install --no-save
```

## Đóng gói / Kiểm thử (Bun)
```sh
bun run build
bun run vitest run
```

## Lưu ý về các kịch bản cài đặt (Lifecycle scripts)
Bun có thể chặn các kịch bản cài đặt của các thư viện phụ thuộc trừ khi bạn cấp quyền tin tưởng rõ ràng. Tuy nhiên, với Moltbot, các kịch bản thường bị chặn này không quá quan trọng (chỉ là các bước kiểm tra phiên bản Node hoặc in cảnh báo).

Nếu bạn gặp lỗi thực tế khi chạy, hãy cấp quyền tin tưởng bằng lệnh:
```sh
bun pm trust @whiskeysockets/baileys protobufjs
```

---
Tài liệu liên quan: [Cài đặt Node.js](./node.vi.md), [Cập nhật hệ thống](./updating.vi.md).
