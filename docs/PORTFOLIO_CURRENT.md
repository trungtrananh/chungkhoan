# Danh mục hiện tại — snapshot 2026-10-09 09:16

> Nguồn: ảnh danh mục do người dùng cung cấp. Đây là **snapshot intraday**, không phải EOD.

## Tổng quan

- Tổng giá trị vốn: **41.122.907 VND**
- Tổng giá trị thị trường: **26.740.450 VND**
- Lãi/lỗ trong ngày: **+245.800 VND (+0,93%)**
- Lãi/lỗ danh mục: **-14.382.457 VND (-34,97%)**

## Holdings

| Mã | KL | KL giao dịch | Giá TT (kVND) | Giá vốn (kVND) | Tỷ trọng | Ngày | Tổng P/L |
|---|---:|---:|---:|---:|---:|---:|---:|
| FPT | 152 | 152 | 59.60 | 98.27 | 33.90% | -0.17% | -39.35% |
| FPT_WFT | 25 | 0 | 59.60 | 0.00 | 5.58% | -0.17% | +1,49 triệu VND |
| HPG | 130 | 130 | 20.20 | 23.70 | 9.82% | +0.25% | -14.78% |
| MBB | 230 | 230 | 18.75 | 22.33 | 16.13% | -0.79% | -16.04% |
| PLX | 100 | 100 | 37.95 | 38.76 | 14.20% | +0.93% | -2.09% |
| PNJ | 285 | 285 | 19.15 | 49.45 | 20.36% | +4.93% | -61.37% |

## Thay đổi so với 08/10 10:08

- **PVB: 100 → 0**; giao dịch bán 100 cp @21.10 đã được người dùng xác nhận ngày 08/10.
- FPT, FPT_WFT, HPG, MBB, PLX, PNJ: quantity không đổi.
- **GVR không xuất hiện trong danh mục**. Lệnh LO 100 cp @33.80 ngày 08/10 vì vậy không được coi là đã khớp.
- Tỷ trọng hiện tại lớn nhất: **FPT + FPT_WFT ~39,48%**, sau đó **PNJ 20,36%**, **MBB 16,13%**.

## Trạng thái giao dịch

- PVB: **đã đóng vị thế**.
- GVR: **không có vị thế được quan sát trong snapshot**.
- Không có pending order nào được coi là active dựa trên bằng chứng hiện tại.

## Quy tắc cho Agent tiếp theo

1. Dùng `data/portfolio/current_state.json` cho trạng thái hiện biết.
2. Dùng `latest.json` để lấy đầy đủ giá/tỷ trọng/P&L snapshot 09/10 09:16.
3. Không suy diễn GVR đã khớp nếu chưa có xác nhận hoặc snapshot có vị thế.
4. Không lưu số tài khoản chứng khoán hiển thị trong ảnh.

## Giao dịch xác nhận sau snapshot 09:16

- **PNJ: SELL 50 cp @19.50 kVND/cp — FILLED**.
- Giá trị khớp gộp: **975.000 VND**, chưa trừ phí/thuế.
- PNJ hiện còn **235 cp** theo trạng thái hiện biết.
- Các tỷ trọng/P&L trong bảng snapshot 09:16 chưa phản ánh giao dịch này.
