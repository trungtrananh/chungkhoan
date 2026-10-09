# Snapshot Sources

## user_screenshot_2026-10-07_1112

- Ngày theo ngữ cảnh: **2026-10-07**
- Giờ hiển thị trên ảnh: **11:12**
- Loại: ảnh chụp màn hình danh mục do người dùng cung cấp.
- Snapshot intraday.
- Account identifier xuất hiện trên ảnh nhưng **không được lưu** vào dữ liệu repo.

## user_screenshot_2026-10-08_1008

- Ngày theo ngữ cảnh: **2026-10-08**
- Giờ hiển thị trên ảnh: **10:08**
- Loại: ảnh chụp màn hình danh mục do người dùng cung cấp.
- Snapshot intraday.
- Account identifier xuất hiện trên ảnh nhưng **không được lưu** vào dữ liệu repo.

## Provenance rule

Các con số trong CSV/JSON phải trace được về một source_id ở file này. Nếu dữ liệu là suy ra (ví dụ bán 100 cp vì quantity giảm 252 → 152), phải ghi `inferred` và không biến giá khớp thành fact.

## user_message_2026-10-08_1406

- Ngày theo ngữ cảnh: **2026-10-08**
- Giờ hội thoại: khoảng **14:06**.
- Loại: xác nhận trực tiếp từ người dùng, không phải screenshot.
- Người dùng xác nhận:
  - **PVB SELL 100 cp @ 21.10 kVND/cp — FILLED**.
  - **GVR BUY LO 100 cp @ 33.80 kVND/cp — PENDING**.
- Chỉ PVB được coi là giao dịch đã thực hiện. GVR chưa được tính vào holdings cho tới khi có xác nhận khớp.

## user_screenshot_2026-10-09_0916

- Ngày theo ngữ cảnh: **2026-10-09**
- Giờ hiển thị trên ảnh: **09:16**
- Loại: ảnh chụp màn hình danh mục do người dùng cung cấp.
- Snapshot intraday.
- Tổng giá trị vốn: **41.122.907 VND**.
- Tổng giá trị thị trường: **26.740.450 VND**.
- P/L ngày: **+245.800 VND (+0,93%)**.
- P/L danh mục: **-14.382.457 VND (-34,97%)**.
- PVB không còn xuất hiện; phù hợp với giao dịch bán đã được xác nhận ngày 08/10.
- GVR không xuất hiện; prior LO 100 @33.80 không được coi là đã khớp.
- Account identifier xuất hiện trên ảnh nhưng **không được lưu** vào dữ liệu repo.
