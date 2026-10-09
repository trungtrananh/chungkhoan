# Portfolio + Scanner Harness Architecture

## Mục tiêu

Thiết kế repo để Agent có thể nạp nhanh:
1. trạng thái danh mục;
2. rule scan/trade hiện hành;
3. prediction history/calibration;
4. provenance dữ liệu.

## Cấu trúc

```text
/
├── AGENTS.md
├── README.md
├── skills/
│   └── chungkhoan/
│       ├── AGENTS.md
│       ├── SKILL.md
│       ├── README.md
│       ├── CHANGELOG.md
│       └── templates/
│           ├── SCAN_REPORT_TEMPLATE.md
│           └── INTRADAY_TRADE_PLAN_TEMPLATE.md
├── docs/
│   ├── HARNESS.md
│   ├── HIGH_CONVICTION_FRAMEWORK.md
│   └── PORTFOLIO_CURRENT.md
└── data/
    ├── portfolio/
    │   ├── current_state.json
    │   ├── latest.json
    │   ├── holdings_history.csv
    │   ├── snapshot_summary.csv
    │   ├── transactions_confirmed.csv
    │   ├── transactions_inferred.csv
    │   ├── pending_orders.csv
    │   └── SOURCES.md
    └── scanner/
        ├── README.md
        └── predictions.csv
```

## Entry points

### Phân tích/quét/trade
Đọc `skills/chungkhoan/SKILL.md`.

### Danh mục hiện tại
Đọc `data/portfolio/current_state.json`.

### Snapshot ảnh gần nhất
Đọc `data/portfolio/latest.json`.

### Track record scanner
Đọc `data/scanner/predictions.csv`.

## Tầng dữ liệu danh mục

- `current_state.json`: trạng thái hiện biết mới nhất.
- `latest.json`: snapshot ảnh gần nhất.
- `holdings_history.csv`: append-only theo snapshot.
- `snapshot_summary.csv`: tổng P/L theo snapshot.
- `transactions_confirmed.csv`: lệnh đã được người dùng xác nhận.
- `transactions_inferred.csv`: thay đổi suy ra khi chưa có xác nhận trực tiếp.
- `pending_orders.csv`: lệnh chờ, không được coi là holding.

## Tầng scanner

- `skills/chungkhoan/SKILL.md`: logic vận hành.
- `docs/HIGH_CONVICTION_FRAMEWORK.md`: tóm tắt rule.
- `data/scanner/predictions.csv`: append-only prediction ledger.
- Có thể tạo `data/scanner/runs/YYYY-MM-DD.md` để lưu full report.

## Quy tắc provenance

Mỗi snapshot/event phải có source_id.
Nguồn ảnh không cần commit nếu dữ liệu cấu trúc + provenance đã được lưu.

## Quy tắc thời gian

- Snapshot intraday phải ghi giờ và **không** diễn giải là EOD.
- Official High-Conviction prediction chỉ phát sau phiên khi đủ dữ liệu.
- Pending order không được biến thành holding.

## Quy tắc versioning skill

Khi thay đổi gate/rule:
1. update `skills/chungkhoan/SKILL.md`;
2. tăng version;
3. ghi `skills/chungkhoan/CHANGELOG.md`;
4. đồng bộ `docs/HIGH_CONVICTION_FRAMEWORK.md`;
5. không hồi tố prediction cũ.

## Bảo mật

Không commit:
- số tài khoản chứng khoán;
- mật khẩu/PIN/OTP;
- credential;
- dữ liệu nhận dạng không cần thiết.
