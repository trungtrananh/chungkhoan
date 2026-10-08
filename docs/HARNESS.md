# Portfolio Harness Architecture

## Mục tiêu

Thiết kế repo để Agent có thể nạp nhanh **trạng thái hiện tại**, sau đó drill-down vào lịch sử mà không cần đọc hàng trăm tin nhắn.

## Cấu trúc

```text
/
├── AGENTS.md
├── README.md
├── docs/
│   ├── HARNESS.md
│   ├── HIGH_CONVICTION_FRAMEWORK.md
│   └── PORTFOLIO_CURRENT.md
└── data/
    └── portfolio/
        ├── README.md
        ├── SOURCES.md
        ├── latest.json
        ├── holdings_history.csv
        ├── snapshot_summary.csv
        └── transactions_inferred.csv
```

## Tầng dữ liệu

### 1. latest.json
Dùng cho truy vấn nhanh nhất. Chỉ chứa snapshot mới nhất, có timestamp và danh sách holdings.

### 2. holdings_history.csv
Bảng append-only theo khóa:
`snapshot_date + snapshot_time + ticker`.

Không ghi đè lịch sử.

### 3. snapshot_summary.csv
Một dòng cho mỗi snapshot: P/L ngày, P/L toàn danh mục, ước tính market value của các vị thế đang hiển thị.

### 4. transactions_inferred.csv
Không phải sổ lệnh chính thức. Chỉ lưu **giao dịch suy ra từ thay đổi quantity** giữa hai snapshot.
Giá khớp để trống nếu chưa có bằng chứng.

## Tầng ngữ nghĩa

- `PORTFOLIO_CURRENT.md`: Agent đọc nhanh trạng thái.
- `HIGH_CONVICTION_FRAMEWORK.md`: logic ra quyết định/scanner.
- `AGENTS.md`: guardrails và quy trình cập nhật.

## Quy tắc provenance

Mỗi snapshot có `source_id`.
Nguồn ảnh không nhất thiết được commit vào repo; dữ liệu cấu trúc được trích từ ảnh và provenance được lưu trong `SOURCES.md`.

## Quy tắc thời gian

Snapshot intraday phải ghi đúng giờ, ví dụ `2026-10-08 10:08`, và **không được diễn giải là EOD**.

## Quy tắc bảo mật

Không commit:
- số tài khoản chứng khoán;
- mật khẩu/PIN/OTP;
- thông tin đăng nhập;
- dữ liệu nhận dạng không cần cho phân tích danh mục.
