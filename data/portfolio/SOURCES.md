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
