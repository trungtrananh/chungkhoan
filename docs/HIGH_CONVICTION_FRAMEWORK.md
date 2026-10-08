# High-Conviction Stock Scanner — Current Rules

## Horizon
7 **phiên giao dịch** tiếp theo.

## Điều kiện để phát prediction
Một mã chỉ được chọn nếu đồng thời:
- High-Conviction Score >= 80/100;
- Estimated Confidence > 80%;
- Expected upside >= 5%;
- Risk/Reward >= 2;
- không có red flag nghiêm trọng.

Tối đa 3 mã; **0 mã là output hợp lệ**.

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

## Calibration
Không được xem Estimated Confidence như xác suất thống kê được bảo đảm.

Prediction mới theo ngưỡng hiện hành:
- WIN nếu giá chạm ít nhất +5% so với reference trong 7 phiên;
- LOSS nếu không chạm;
- không hồi tố thay đổi tiêu chí;
- không thay target/reference/horizon sau khi biết diễn biến.

## Bài học đã khóa
- Fundamental target 12 tháng không được dùng để suy ra +5%/7D.
- Breakout cần follow-through + volume + flow confirmation.
- Market regime penalty có thể loại một stock setup đẹp.
- Corporate action phải điều chỉnh giá trước TA.
- Không chase sau expansion candle nếu R/R <2.
- No trade is a valid position.
