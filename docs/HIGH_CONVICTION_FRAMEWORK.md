# High-Conviction Stock Scanner — Current Rules

> **Canonical runbook:** `skills/chungkhoan/SKILL.md`  
> File này là bản tóm tắt nhanh. Nếu có khác biệt, ưu tiên `SKILL.md`.

## Horizon
7 **phiên giao dịch** tiếp theo.

## Điều kiện để phát prediction
Một mã chỉ được chọn nếu đồng thời:
- High-Conviction Score >= 80/100;
- Estimated Confidence > 80%;
- Expected upside >= 5%;
- Risk/Reward >= 2;
- không có red flag nghiêm trọng;
- dữ liệu đủ để kiểm chứng;
- Market Regime không phủ định thesis.

Tối đa 3 mã; **0 mã là output hợp lệ**. Không làm tròn 79.x thành 80.

## Watch thresholds
- 80+: High-Conviction **chỉ khi toàn bộ gates đạt**
- 77–79.9: Watch #1 / sát ngưỡng
- 73–76.9: Watch
- <73: Reject hoặc theo dõi xa
- Red Flag: loại khỏi long scanner tới khi được giải quyết

## Nhóm bằng chứng bắt buộc

Scanner phải xem xét:
- Market Regime / VN-Index;
- vĩ mô Việt Nam;
- global macro/risk;
- sector rotation và relative strength;
- fundamentals;
- catalyst và catalyst timing;
- price-in;
- technical / market structure;
- volume-price action;
- Wyckoff;
- Smart Money Concepts;
- foreign / tự doanh / institutional flow nếu có;
- crowd sentiment / hype risk;
- bear case / anti-confirmation bias;
- liquidity / manipulation / dilution / legal red flags.

## EOD vs Intraday
- **Official prediction chỉ phát sau phiên**, khi đủ dữ liệu EOD.
- Intraday chỉ là tactical trade plan; không ghi vào prediction ledger.
- Nếu EOD chưa đồng bộ, nói rõ và không giả dữ liệu.

## Calibration
Không được xem Estimated Confidence như xác suất thống kê được bảo đảm.

Prediction mới theo skill v1:
- WIN nếu giá chạm ít nhất +5% so với reference trong 7 phiên;
- LOSS nếu không chạm;
- không hồi tố thay đổi tiêu chí;
- không thay target/reference/horizon sau khi biết diễn biến.

Prediction ledger: `data/scanner/predictions.csv`.

## Bài học đã khóa
- Fundamental target 12 tháng không được dùng để suy ra +5%/7D.
- Breakout cần follow-through + volume + flow confirmation.
- Market regime penalty có thể loại một stock setup đẹp.
- Corporate action phải điều chỉnh giá trước TA.
- Không chase sau expansion candle nếu R/R <2.
- ETF/index flow có thể là mechanical, không mặc định là smart-money conviction.
- No trade / cash là một vị thế hợp lệ.
