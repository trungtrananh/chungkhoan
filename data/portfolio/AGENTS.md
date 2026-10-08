# AGENTS.md — Portfolio Data Local Rules

Áp dụng cho mọi file trong `data/portfolio/`.

## Mutation rules
- `holdings_history.csv`: append-only theo snapshot; không sửa lịch sử trừ khi có bằng chứng nguồn rõ ràng.
- `snapshot_summary.csv`: mỗi snapshot đúng 1 dòng.
- `latest.json`: luôn thay thế bằng snapshot ảnh mới nhất sau khi append history.
- `current_state.json`: cập nhật khi có giao dịch được người dùng xác nhận sau snapshot; đây là trạng thái hiện biết mới nhất.
- `transactions_confirmed.csv`: giao dịch do người dùng xác nhận đã khớp; lưu đúng giá/khối lượng được xác nhận.
- `transactions_inferred.csv`: chỉ thêm giao dịch khi quantity thay đổi giữa hai snapshot mà chưa có xác nhận trực tiếp; không tự điền execution price.
- `pending_orders.csv`: lệnh chưa khớp; không cộng vào holdings.
- `SOURCES.md`: thêm source_id cho mọi ảnh/file mới.

## Validation checklist
- Tổng quantity từng mã phải khớp ảnh nguồn.
- `tradable_quantity` phải tách khỏi `quantity` nếu UI cho thấy cổ phiếu chưa về/chưa giao dịch được.
- Giá dùng kVND/cp.
- Snapshot intraday không được gắn nhãn EOD.
- P/L VND từ UI có thể là số làm tròn; không “sửa” bằng phép tính nếu nguồn hiển thị khác.
- Không lưu account number, OTP, PIN hoặc credential.

## Query pattern
- current known state: `current_state.json`
- latest screenshot snapshot: `latest.json`
- point-in-time history: filter `holdings_history.csv`
- portfolio P/L over time: `snapshot_summary.csv`
- confirmed trades: `transactions_confirmed.csv`
- inferred position changes: `transactions_inferred.csv`
- active pending orders: `pending_orders.csv`
