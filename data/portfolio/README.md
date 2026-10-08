# Portfolio Data

## Units

- `market_price_kvnd`, `cost_basis_kvnd`, `execution_price_kvnd`: nghìn VND/cổ phiếu.
- `*_pnl_vnd`, `estimated_positions_market_value_vnd`: VND.
- `quantity`, `tradable_quantity`: số cổ phiếu.
- Phần trăm lưu dưới dạng số, ví dụ `-34.29` = -34,29%.

## Files

- `latest.json`: snapshot mới nhất.
- `holdings_history.csv`: lịch sử holdings.
- `snapshot_summary.csv`: tổng P/L theo snapshot.
- `transactions_inferred.csv`: giao dịch suy ra từ delta quantity.
- `SOURCES.md`: provenance.

## Important

`transactions_inferred.csv` không thay thế lịch sử lệnh từ broker.
Nếu execution price không được cung cấp/xác minh thì để trống.
