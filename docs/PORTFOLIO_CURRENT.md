# Danh mục hiện tại — snapshot 12/10/2026 10:00

Ngày gán theo ngữ cảnh hội thoại; ảnh không hiện ngày. Giờ 10:00 trực tiếp từ ảnh. Snapshot intraday, không phải EOD. Nguồn: `user_screenshot_2026-10-12_1000`.

- Tổng vốn: **38.650.544 VND**.
- Giá trị thị trường: **25.487.850 VND**.
- P/L ngày: **-72.450 VND (-0,28%)**.
- P/L danh mục: **-13.162.694 VND (-34,06%)**.

| Mã | KL | Khả dụng | Giá TT (kVND) | Giá vốn (kVND) | Tỷ trọng | P/L ngày | P/L tổng |
|---|---:|---:|---:|---:|---:|---:|---:|
| FPT | 152 | 152 | 58.30 | 98.27 | 34.71% | 0.69% | -40.77% |
| FPT_WFT | 25 | 0 | 58.30 | 0.00 | 5.72% | 0.69% | +1,46 triệu VND |
| HPG | 130 | 130 | 20.20 | 23.70 | 10.30% | 0.50% | -14.78% |
| MBB | 230 | 230 | 19.15 | 22.33 | 17.28% | 0.52% | -14.25% |
| PLX | 100 | 100 | 36.85 | 38.76 | 14.47% | -1.34% | -4.93% |
| PNJ | 235 | 235 | 18.95 | 49.45 | 17.47% | -2.82% | -61.68% |

## Đối chiếu lịch sử

PNJ 285 → 235 so với ảnh 09/10 09:16, phù hợp bán 50 cp @19,50 đã xác nhận lúc 09:20; không ghi trùng giao dịch. Các mã còn lại không đổi số lượng. PVB đã bán theo xác nhận cũ. GVR không xuất hiện; không kết luận lệnh cũ đã hủy hoặc đã khớp.

P/L danh mục ít âm hơn ảnh 09/10 khoảng 1.219.763 VND, nhưng hai snapshot khác số lượng do bán PNJ; không coi chênh lệch này là lợi nhuận đầu tư của tài khoản. Giá trị thị trường giảm 1.252.600 VND, tổng vốn giảm 2.472.363 VND.

FPT + FPT_WFT chiếm **40,43% giá trị cổ phiếu**, không phải tỷ trọng tổng tài sản vì thiếu tiền mặt. FPT_WFT không khả dụng để bán. Chưa có tiền mặt/margin hoặc trạng thái lệnh mới. Tổng vốn tính từ giá vốn làm tròn cao hơn UI 146 VND; giữ tổng UI. Tỷ trọng hiển thị cộng thành 99,95%.

## Cách đọc

Dùng current_state.json cho số lượng hiện biết; latest.json cho giá/P&L gốc 10:00. Báo cáo thị trường buổi chiều ở data/scanner/runs/2026-10-12.md là Analysis, không sửa ảnh nguồn và không tạo giao dịch.

## Xác nhận ngày 13/10/2026 và định giá EOD

Người dùng xác nhận **không có giao dịch mới ngày 12/10**. Số lượng giữ nguyên. Theo giá đóng cửa thị trường 12/10 và giả định WFT theo giá FPT, giá trị cổ phiếu **ước tính 25.087.450 VND**, tỷ trọng FPT-family **40,29%**. Đây là Analysis, không phải snapshot/P&L từ công ty chứng khoán. Giá và P/L trong bảng trên vẫn thuộc ảnh 10:00. Xem data/portfolio/valuations/2026-10-12.json và data/scanner/runs/2026-10-12-eod-plan-2026-10-13.md.
