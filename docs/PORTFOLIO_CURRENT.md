# Danh mục hiện biết — 2026-10-08 14:06

> Trạng thái này được dựng từ **snapshot ảnh 10:08** cộng các giao dịch/lệnh người dùng xác nhận sau snapshot. Snapshot gốc vẫn được giữ nguyên trong `latest.json`.

## Holdings hiện biết

| Mã | KL hiện biết | Ghi chú |
|---|---:|---|
| FPT | 152 | Không có giao dịch mới sau snapshot |
| FPT_WFT | 25 | Snapshot 10:08 cho thấy KL giao dịch = 0 |
| HPG | 130 | Không đổi |
| MBB | 230 | Không đổi |
| PLX | 100 | Không đổi |
| PNJ | 285 | Không đổi |
| PVB | **0** | Đã bán nốt 100 cp |

## Giao dịch xác nhận sau snapshot

- **PVB: SELL 100 cp @ 21.10 kVND/cp — FILLED**
- Giá trị khớp gộp: **2.110.000 VND**, chưa trừ phí/thuế.
- Đây là xác nhận trực tiếp của người dùng, không phải suy luận từ ảnh.

## Lệnh đang chờ

- **GVR: BUY LO 100 cp @ 33.80 kVND/cp — PENDING**
- **Chưa tính GVR vào danh mục** cho tới khi người dùng xác nhận lệnh đã khớp.

## Snapshot ảnh gần nhất — 2026-10-08 10:08

- Lãi/lỗ trong ngày: **+211.700 VND (+0,74%)**
- Lãi/lỗ danh mục: **-15.073.552 VND (-34,29%)**
- Estimated market value các vị thế hiển thị lúc 10:08: **~28,884 triệu VND**
- Các tỷ trọng/P&L này **đã stale sau giao dịch PVB lúc 14:06**; không tự tính lại nếu chưa có snapshot đầy đủ mới.

## Thay đổi đã biết từ 07/10 đến hiện tại

- FPT: **252 → 152** ⇒ giảm 100 cp (giá khớp chưa được xác nhận trong dữ liệu repo).
- PVB: **200 → 100** qua snapshot 08/10 10:08; sau đó **100 → 0**, bán xác nhận @21.10.
- HPG, MBB, PLX, PNJ, FPT_WFT: quantity chưa có bằng chứng thay đổi.
- GVR hiện chỉ là **lệnh mua đang chờ**, chưa phải holding.

## Quy tắc cho Agent tiếp theo

1. Đọc `data/portfolio/current_state.json` trước.
2. Không dùng tỷ trọng từ snapshot 10:08 như tỷ trọng hiện tại sau khi PVB đã bán.
3. Không tính GVR vào holdings nếu chưa có xác nhận FILLED.
4. Khi có ảnh danh mục mới, snapshot ảnh mới sẽ supersede trạng thái suy diễn hiện tại và cần reconcile với các transaction đã xác nhận.
