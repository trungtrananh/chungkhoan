# AGENTS.md — Portfolio Data Local Rules

Áp dụng cho mọi file trong `data/portfolio/`.

## Mutation rules
- `holdings_history.csv`: append-only theo snapshot; không sửa lịch sử trừ khi có bằng chứng nguồn rõ ràng.
- `snapshot_summary.csv`: mỗi snapshot đúng 1 dòng.
- `latest.json`: luôn thay thế bằng snapshot mới nhất sau khi append history.
- `transactions_inferred.csv`: chỉ thêm giao dịch khi quantity thay đổi giữa hai snapshot; không tự điền execution price.
- `SOURCES.md`: thêm source_id cho mọi ảnh/file mới.

## Validation checklist
- Tổng quantity từng mã phải khớp ảnh nguồn.
- `tradable_quantity` phải tách khỏi `quantity` nếu UI cho thấy cổ phiếu chưa về/chưa giao dịch được.
- Giá dùng kVND/cp.
- Snapshot intraday không được gắn nhãn EOD.
- P/L VND từ UI có thể là số làm tròn; không “sửa” bằng phép tính nếu nguồn hiển thị khác.
- Không lưu account number, OTP, PIN hoặc credential.

## Query pattern
- latest state: `latest.json`
- point-in-time history: filter `holdings_history.csv`
- portfolio P/L over time: `snapshot_summary.csv`
- observed position changes: `transactions_inferred.csv`
