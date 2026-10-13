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

## user_message_2026-10-09_0920

- Ngày theo ngữ cảnh: **2026-10-09**.
- Giờ hội thoại: khoảng **09:20**.
- Loại: xác nhận trực tiếp từ người dùng.
- Người dùng xác nhận **PNJ SELL 50 cp @19.50 kVND/cp — FILLED**.
- Sau giao dịch, PNJ còn **235 cp** theo trạng thái hiện biết.

## user_screenshot_2026-10-12_1000

- Ngày gán theo ngữ cảnh hội thoại: **2026-10-12**, chưa xác nhận từ ảnh (ảnh không hiện ngày).
- Giờ hiển thị: **10:00**; snapshot intraday, không phải EOD.
- Loại: ảnh danh mục do người dùng gửi; không commit ảnh có số tài khoản.
- Tổng vốn 38.650.544 VND; thị trường 25.487.850 VND.
- P/L ngày -72.450 VND (-0,28%); danh mục -13.162.694 VND (-34,06%).
- FPT 152; FPT_WFT 25 (khả dụng 0); HPG 130; MBB 230; PLX 100; PNJ 235.
- PNJ giảm 50 cp so với snapshot 09/10 09:16, nhưng khớp giao dịch đã xác nhận lúc 09:20 cùng ngày. Không thêm giao dịch suy ra hoặc giao dịch xác nhận mới.
- Không suy ra tiền mặt, margin, phí/thuế, giá khớp mới hoặc trạng thái lệnh GVR từ ảnh này.
- Giá vốn từng dòng làm tròn; tổng vốn tính lại lệch 146 VND; giữ nguyên số tổng trên UI.
- Account identifier không được lưu.

## user_message_2026-10-13_no_trades_2026-10-12

- Người dùng xác nhận ngày 13/10/2026: ngày 12/10 không thực hiện thêm giao dịch nào.
- Giữ nguyên số lượng đã biết; không thêm giao dịch xác nhận/suy ra hoặc snapshot ảnh mới.
- Không xác nhận tiền mặt, margin, trạng thái lệnh hoặc availability của WFT.
- Ước tính giá trị EOD từ thị trường được lưu riêng ở valuations/2026-10-12.json, không thay latest.json.
