# AGENTS.md — Chứng khoán Portfolio Harness

## Mục đích

Repo này là **source of truth dài hạn** cho:
- lịch sử danh mục chứng khoán của người dùng;
- các thay đổi vị thế quan sát được từ ảnh chụp/tài liệu người dùng cung cấp;
- framework High-Conviction Stock Scanner;
- ghi chú để Agent khác có thể tiếp tục phân tích mà không phải đọc lại toàn bộ hội thoại.

## Nguyên tắc dữ liệu

1. **Không suy đoán dữ liệu danh mục nếu ảnh/tài liệu không thể hiện.**
2. Giá cổ phiếu trong ảnh app được lưu theo đơn vị **nghìn VND/cp (kVND)**, ví dụ `60.80` = 60.800 VND/cp.
3. Khối lượng là **số cổ phiếu**.
4. Các trường P/L được lưu đúng như ảnh chụp. Sai số làm tròn từ UI được giữ nguyên.
5. `FPT_WFT` hiện được ghi nhận như một vị thế/chứng khoán chờ về hoặc quyền liên quan FPT; nếu `tradable_quantity=0` thì **không được coi là cổ phiếu có thể bán ngay**.
6. Chỉ suy ra giao dịch từ chênh lệch số lượng giữa hai snapshot khi bằng chứng rõ ràng. **Không suy ra giá khớp** nếu không có xác nhận.
7. Khi có corporate action (cổ tức cổ phiếu, chia tách, quyền mua...), phải dùng **adjusted-price series** trước khi đọc Technical/Wyckoff/SMC.
8. Không lưu số tài khoản chứng khoán, thông tin đăng nhập hoặc dữ liệu nhận dạng không cần thiết.

## Source of truth

Đọc theo thứ tự:
1. `data/portfolio/current_state.json` — trạng thái hiện biết mới nhất = snapshot gần nhất + giao dịch đã xác nhận sau snapshot.
2. `data/portfolio/latest.json` — snapshot ảnh mới nhất, không tự thay đổi bởi giao dịch xác nhận sau ảnh.
3. `data/portfolio/holdings_history.csv` — lịch sử từng mã theo từng snapshot.
4. `data/portfolio/snapshot_summary.csv` — P/L tổng danh mục theo thời điểm.
5. `data/portfolio/transactions_confirmed.csv` — giao dịch người dùng xác nhận đã khớp.
6. `data/portfolio/transactions_inferred.csv` — giao dịch **suy ra** từ thay đổi số lượng.
7. `data/portfolio/pending_orders.csv` — lệnh đang chờ, không được tính là holding.
8. `docs/PORTFOLIO_CURRENT.md` — bản tóm tắt cho người/Agent.
9. `docs/HIGH_CONVICTION_FRAMEWORK.md` — logic scanner.
10. `docs/HARNESS.md` — kiến trúc và cách cập nhật.

## Quy trình cập nhật snapshot mới

Khi người dùng gửi ảnh danh mục mới:
1. Đọc timestamp hiển thị trên ảnh và ngày theo ngữ cảnh cuộc trò chuyện.
2. Thêm từng mã vào `holdings_history.csv`.
3. Thêm P/L tổng vào `snapshot_summary.csv`.
4. So sánh quantity với snapshot gần nhất:
   - nếu thay đổi, thêm một dòng vào `transactions_inferred.csv`;
   - `execution_price_kvnd` để trống nếu ảnh không chứng minh giá khớp;
   - mô tả bằng chứng ở `evidence_note`.
5. Thay thế `latest.json` bằng snapshot mới nhất.
6. Cập nhật `docs/PORTFOLIO_CURRENT.md`.
7. Không xóa snapshot lịch sử.

## High-Conviction Scanner

Tiêu chuẩn hiện hành cho **prediction mới**:
- High-Conviction Score >= 80/100;
- Estimated Confidence > 80%;
- Expected upside >= 5% trong **7 phiên giao dịch**;
- Risk/Reward >= 2;
- không có red flag nghiêm trọng;
- không ép đủ 3 mã.

Nếu không có mã đạt chuẩn, output hợp lệ là **0 mã**.

### Track record

- Prediction mới theo framework hiện tại: **WIN nếu chạm +5% trong cửa sổ 7 phiên**.
- Không hồi tố prediction cũ đã phát hành theo tiêu chí khác.
- Không thay reference price, target hay kéo dài cửa sổ sau khi prediction đã phát hành.
- Phải theo dõi MFE, MAE, giá cuối kỳ và lesson từ prediction sai.
- Confidence phải được calibration theo hit rate thực tế; sample nhỏ phải ghi rõ `n`.

## Phân biệt dữ liệu và nhận định

- **Observed:** trực tiếp từ ảnh/file/nguồn xác nhận.
- **Inferred:** suy ra hợp lý từ observed data, phải gắn nhãn.
- **Analysis:** nhận định đầu tư; không ghi như fact.
- Giá vốn lịch sử không phải lý do tự thân để mua/giữ/bán; quyết định dựa trên expected return/risk từ hiện tại.

## Truy vấn nhanh

- “Danh mục mới nhất?” → đọc `data/portfolio/current_state.json`; dùng `latest.json` để xem snapshot ảnh gốc gần nhất.
- “Hôm qua so với hôm nay thay đổi gì?” → đọc 2 ngày gần nhất trong `holdings_history.csv` + `transactions_inferred.csv`.
- “Tỷ trọng mã nào lớn nhất?” → dùng `weight_pct` snapshot mới nhất.
- “Đã bán bao nhiêu FPT/PVB?” → ưu tiên `transactions_confirmed.csv`; chỉ dùng `transactions_inferred.csv` khi chưa có xác nhận trực tiếp.
- “Có lệnh nào đang chờ?” → đọc `pending_orders.csv`; **không** biến lệnh PENDING thành holding.
