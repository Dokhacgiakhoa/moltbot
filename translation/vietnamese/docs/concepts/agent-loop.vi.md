---
summary: "Vòng đời của vòng lặp Agent, luồng dữ liệu và cơ chế chờ đợi"
read_when:
  - Bạn cần tìm hiểu chi tiết quy trình của vòng lặp Agent hoặc các sự kiện vòng đời
---

# Vòng lặp Agent (Agent Loop)

Vòng lặp Agent là quy trình thực thi đầy đủ của một Agent: tiếp nhận dữ liệu → lắp ghép ngữ cảnh → mô hình AI suy luận → thực thi công cụ → phản hồi trực tiếp (streaming) → lưu trữ dữ liệu. Đây là con đường chính thức biến một tin nhắn thành hành động và câu trả lời cuối cùng, đồng thời giữ cho trạng thái phiên làm việc luôn nhất quán.

Trong Moltbot, mỗi vòng lặp là một lượt chạy tuần tự cho mỗi phiên làm việc, phát ra các sự kiện vòng đời và luồng dữ liệu khi mô hình đang suy nghĩ, gọi công cụ và trả về kết quả.

## Các điểm truy cập
- Gateway RPC: lệnh `agent` và `agent.wait`.
- CLI: lệnh `moltbot agent`.

## Cách thức hoạt động (Cấp độ hệ thống)
1) **Yêu cầu RPC `agent`**: Kiểm tra các tham số, xác định phiên làm việc (sessionKey/sessionId), lưu trữ thông tin về phiên và trả về ngay lập tức mã `{ runId, acceptedAt }`.
2) **Thực thi lệnh Agent**:
   - Xác định mô hình AI và các tùy chọn suy luận/hiển thị chi tiết.
   - Tải các "ảnh chụp" kỹ năng (skills snapshot).
   - Gọi trình thực thi `runEmbeddedPiAgent`.
   - Phát sự kiện **kết thúc/lỗi** nếu vòng lặp nhúng gặp sự cố.
3) **Hàm `runEmbeddedPiAgent`**:
   - Xếp hàng các lượt chạy để thực hiện tuần tự theo từng phiên làm việc.
   - Xác định mô hình và hồ sơ xác thực.
   - Đăng ký nhận các sự kiện và truyền các thay đổi (deltas) từ trợ lý/công cụ.
   - Áp dụng thời gian chờ (timeout) -> hủy lượt chạy nếu quá hạn.
4) **Hàm `agent.wait`**:
   - Chờ đợi sự kiện **kết thúc/lỗi** cho một mã `runId` cụ thể.
   - Trả về trạng thái `{ status: ok|error|timeout, startedAt, endedAt, error? }`.

## Xếp hàng & Đồng thời (Concurrency)
- Các lượt chạy được thực hiện tuần tự cho mỗi phiên làm việc (session lane) để tránh việc các công cụ bị xung đột và giữ cho lịch sử phiên luôn đúng thứ tự.
- Các kênh nhắn tin có thể chọn chế độ hàng đợi (collect/steer/followup) để nạp dữ liệu vào hệ thống này. Xem thêm tại [Hàng đợi lệnh](./queue.vi.md).

## Lắp ghép câu lệnh (Prompt)
- Câu lệnh hệ thống được xây dựng từ: câu lệnh gốc của Moltbot, câu lệnh của kỹ năng, ngữ cảnh khởi tạo (bootstrap) và các ghi đè riêng cho từng lượt chạy.
- Các giới hạn của từng mô hình và quy tắc nén ngữ cảnh (compaction) sẽ được áp dụng tại đây.

## Các điểm can thiệp (Hooks)
Moltbot có hai hệ thống can thiệp:
- **Internal hooks**: Các kịch bản tự động hóa cho lệnh và sự kiện vòng đời.
- **Plugin hooks**: Các điểm mở rộng sâu bên trong vòng đời Agent/Công cụ.

Ví dụ: `agent:bootstrap` chạy trong lúc xây dựng các tệp khởi tạo trước khi câu lệnh hệ thống được chốt lại.

Chi tiết tại: [Hooks](../hooks.vi.md).

## Thực thi công cụ
- Các sự kiện bắt đầu/cập nhật/kết thúc công cụ được phát ra qua luồng `tool`.
- Kết quả công cụ được làm sạch (về kích thước và dữ liệu hình ảnh) trước khi lưu nhật ký hoặc phát đi.

## Tóm tắt & Trạng thái
- Câu trả lời cuối cùng được lắp ghép từ: văn bản của trợ lý, tóm tắt công cụ, văn bản lỗi (nếu có).
- Các lượt chạy bị lỗi hoặc quá hạn sẽ được thông báo rõ ràng để người dùng xử lý.

---
Tài liệu liên quan: [Cấu hình truyền tin](./streaming.vi.md), [Nén ngữ cảnh](./compaction.vi.md).
