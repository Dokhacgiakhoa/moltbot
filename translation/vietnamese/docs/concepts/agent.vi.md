---
summary: "Trình thực thi Agent (nhúng p-mono), quy ước không gian làm việc và khởi tạo phiên làm việc"
read_when:
  - Bạn muốn thay đổi trình thực thi Agent, quy trình khởi tạo không gian làm việc hoặc hành vi phiên làm việc
---

# Trình thực thi Agent (Runtime) 🤖

Moltbot sử dụng một trình thực thi Agent duy nhất được nhúng bên trong, phát triển dựa trên nền tảng **p-mono**.

## Không gian làm việc (Workspace - Bắt buộc)

Moltbot sử dụng một thư mục không gian làm việc duy nhất (`agents.defaults.workspace`) làm thư mục làm việc chính (`cwd`) cho mọi công cụ và ngữ cảnh của Agent.

Khuyên dùng: Sử dụng lệnh `moltbot setup` để tạo tệp cấu hình `~/.clawdbot/moltbot.json` (nếu chưa có) và khởi tạo các tệp tin trong không gian làm việc.

Hướng dẫn chi tiết về sơ đồ thư mục và sao lưu: [Không gian làm việc của Agent](./agent-workspace.vi.md)

Nếu tính năng **sandbox** được bật (`agents.defaults.sandbox`), các phiên làm việc không phải chính (non-main) có thể ghi đè thư mục này bằng các không gian làm việc riêng biệt cho từng phiên (xem thêm tại [Cấu hình Gateway](../gateway/configuration.vi.md)).

## Các tệp khởi tạo (Bootstrap files)

Bên trong thư mục `agents.defaults.workspace`, Moltbot mong đợi các tệp tin có thể chỉnh sửa như sau:
- `AGENTS.md` — Chỉ dẫn hoạt động + "bộ nhớ" của Agent.
- `SOUL.md` — Tính cách, giới hạn và văn phong giao tiếp.
- `TOOLS.md` — Các chú thích về công cụ do người dùng duy trì (ví dụ: các quy ước sử dụng công cụ).
- `BOOTSTRAP.md` — Quy trình "nghi lễ" cho lần chạy đầu tiên (sẽ bị xóa sau khi hoàn thành).
- `IDENTITY.md` — Tên, phong cách và biểu tượng emoji của Agent.
- `USER.md` — Hồ sơ người dùng và cách Agent nên xưng hô với bạn.

Tại lượt gửi đầu tiên của một phiên làm việc mới, Moltbot sẽ nạp nội dung của các tệp này trực tiếp vào ngữ cảnh của Agent.

Các tệp trống sẽ bị bỏ qua. Các tệp quá lớn sẽ được cắt bớt và chèn dấu đánh dấu để giữ cho câu lệnh (prompt) luôn gọn gàng.

Nếu thiếu tệp, Moltbot sẽ chèn một dòng đánh dấu "tệp bị thiếu" (lệnh `moltbot setup` sẽ giúp bạn tạo các tệp mẫu mặc định an toàn).

## Công cụ tích hợp sẵn

Các công cụ cốt lõi (đọc/thực thi/chỉnh sửa/ghi file và các công cụ hệ thống liên quan) luôn sẵn sàng sử dụng, tùy thuộc vào chính sách phân quyền công cụ. Tệp `TOOLS.md` **không** dùng để bật/tắt công cụ; nó chỉ là tài liệu chỉ dẫn cho Agent biết *bạn* muốn chúng được sử dụng như thế nào.

## Các kỹ năng (Skills)

Moltbot tải các kỹ năng từ ba vị trí (nếu trùng tên, không gian làm việc sẽ được ưu tiên):
- Mặc định (đi kèm bộ cài đặt).
- Cục bộ: `~/.clawdbot/skills`.
- Không gian làm việc: `<workspace>/skills`.

## Phiên làm việc (Sessions)

Lịch sử các phiên làm việc được lưu trữ dưới dạng JSONL tại:
`~/.clawdbot/agents/<agentId>/sessions/<SessionId>.jsonl`

ID phiên làm việc là cố định và do Moltbot tự động chọn. Các thư mục phiên làm việc từ các phiên bản Pi/Tau cũ sẽ **không** được sử dụng.

## Điều hướng khi đang truyền tin (Steering while streaming)

Khi chế độ hàng đợi là `steer`, các tin nhắn mới gửi đến sẽ được chèn trực tiếp vào lượt chạy hiện tại. Hàng đợi được kiểm tra **sau mỗi lần gọi công cụ**; nếu có tin nhắn mới, các công cụ còn lại trong thông điệp của Agent sẽ bị bỏ qua (trả về lỗi "Bỏ qua do có tin nhắn chờ từ người dùng"), sau đó tin nhắn mới từ người dùng sẽ được chèn vào trước khi Agent đưa ra phản hồi tiếp theo.

Các chi tiết khác: [Truyền tin & Cắt đoạn (Streaming)](./streaming.vi.md).

## Cấu hình (Tối thiểu)

Để hệ thống hoạt động, bạn cần thiết lập ít nhất:
- `agents.defaults.workspace`: Đường dẫn không gian làm việc.
- `channels.whatsapp.allowFrom`: (Khuyên dùng mạnh mẽ) Danh sách số điện thoại được phép điều khiển.

---
*Tiếp theo: [Trò chuyện nhóm](./group-messages.vi.md)* 🦞
