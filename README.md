# chungkhoan

Kho dữ liệu và harness phục vụ phân tích danh mục chứng khoán Việt Nam.

## Bắt đầu nhanh cho Agent

1. Đọc [AGENTS.md](./AGENTS.md).
2. Đọc trạng thái hiện biết mới nhất: [data/portfolio/current_state.json](./data/portfolio/current_state.json).
3. Đọc snapshot ảnh mới nhất: [data/portfolio/latest.json](./data/portfolio/latest.json).
4. Khi cần lịch sử: [data/portfolio/holdings_history.csv](./data/portfolio/holdings_history.csv).
5. Khi cần thay đổi vị thế: [data/portfolio/transactions_inferred.csv](./data/portfolio/transactions_inferred.csv).
6. Skill dùng hàng ngày: [skills/chungkhoan/SKILL.md](./skills/chungkhoan/SKILL.md).
7. Prediction ledger: [data/scanner/predictions.csv](./data/scanner/predictions.csv).
8. Logic High-Conviction tóm tắt: [docs/HIGH_CONVICTION_FRAMEWORK.md](./docs/HIGH_CONVICTION_FRAMEWORK.md).
9. Kiến trúc harness: [docs/HARNESS.md](./docs/HARNESS.md).

## Snapshot hiện có

- 2026-10-07 11:12 — intraday.
- 2026-10-08 10:08 — intraday.
- 2026-10-09 09:16 — intraday, snapshot ảnh mới nhất.
- 2026-10-08 14:06 — PVB bán 100 @21.10 đã khớp; GVR mua LO 100 @33.80 đã được đặt nhưng không xuất hiện ở snapshot sáng 09/10.

Dữ liệu tài khoản nhạy cảm không được lưu vào repo.

## Skill `chungkhoan`

Có thể yêu cầu Agent thực hiện theo cú pháp tự nhiên hoặc `$chungkhoan`, ví dụ:
- `$chungkhoan quét sau phiên hôm nay`
- `$chungkhoan đánh giá GVR 7 phiên tới`
- `$chungkhoan lập trade plan chiều nay theo danh mục hiện tại`

Skill khóa các ngưỡng High-Conviction và quy tắc calibration để Agent khác dùng nhất quán.
