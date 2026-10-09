# Scanner Data

## predictions.csv
Ledger append-only cho official predictions.

### Quy tắc
- Không sửa reference/target/deadline sau khi phát hành.
- Khi đủ 7 phiên: cập nhật MFE, MAE, status/outcome, lesson.
- Rule/version phải giữ nguyên theo thời điểm prediction được phát hành.
- Prediction intraday không được ghi vào ledger.

## run logging
Nếu cần lưu full report từng ngày, tạo:
`data/scanner/runs/YYYY-MM-DD.md`

Report phải phân biệt:
- dữ liệu EOD đã xác nhận;
- dữ liệu chưa đồng bộ;
- inference/analysis.
