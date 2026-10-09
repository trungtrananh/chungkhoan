---
name: chungkhoan
description: Quét và phân tích thị trường chứng khoán Việt Nam theo High-Conviction framework đã chốt; hỗ trợ scan sau phiên, watchlist, trade plan, quản trị danh mục và track record 7 phiên.
version: 1.0.0
---

# Skill: chungkhoan

## 1. Mục tiêu

Skill này là **runbook chuẩn** cho mọi Agent làm việc với repo `chungkhoan`.

Dùng skill khi người dùng yêu cầu một trong các tác vụ:
- quét cổ phiếu Việt Nam sau phiên;
- tìm tối đa 3 mã High-Conviction;
- cập nhật watchlist/candidate ranking;
- phân tích một mã trong horizon 7 phiên;
- đề xuất chiến lược trade trong ngày dựa trên Market Regime;
- cập nhật prediction, WIN/LOSS, hit rate, calibration;
- phân tích danh mục hiện tại kết hợp dữ liệu repo.

Skill áp dụng cho **HOSE, HNX và UPCoM**.

---

## 2. Nguồn dữ liệu nội bộ bắt buộc đọc trước

Nếu tác vụ liên quan danh mục hoặc lịch sử prediction, đọc theo thứ tự:

1. `/AGENTS.md`
2. `/data/portfolio/current_state.json`
3. `/data/portfolio/latest.json` nếu cần giá/tỷ trọng từ snapshot gần nhất
4. `/data/portfolio/transactions_confirmed.csv`
5. `/data/portfolio/pending_orders.csv`
6. `/data/scanner/predictions.csv`
7. `/docs/HIGH_CONVICTION_FRAMEWORK.md`

Không suy đoán giao dịch, giá vốn, giá khớp hoặc trạng thái lệnh nếu repo/người dùng chưa xác nhận.

---

## 3. Quy tắc thời gian

### Scan chính thức
High-Conviction Stock Scanner là **after-close scanner**.

Chỉ phát prediction chính thức khi đã có dữ liệu đủ đáng tin cậy sau khi phiên giao dịch kết thúc:
- giá đóng cửa;
- volume/thanh khoản;
- breadth/index close;
- foreign flow;
- tự doanh/institutional flow nếu có dữ liệu;
- corporate action trong ngày nếu có.

Nếu nguồn EOD chưa đồng bộ:
- nói rõ dữ liệu chưa hoàn chỉnh;
- có thể cập nhật Market Regime/Watchlist tạm thời;
- **không phát prediction chính thức** từ dữ liệu buổi sáng/giữa phiên.

### Intraday
Trong phiên chỉ được đưa:
- tactical trade plan;
- vùng mua/bán;
- điều kiện xác nhận/hủy lệnh;
- không được chấm High-Conviction prediction chính thức như EOD.

---

## 4. Horizon và điều kiện cứng

### Horizon
**7 phiên giao dịch tiếp theo**, không tính ngày nghỉ.

### High-Conviction gates
Một mã chỉ được phát hành thành prediction khi **đồng thời** đạt:

- High-Conviction Score **>= 80/100**
- Estimated Confidence **> 80%**
- Expected upside **>= 5%** trong 7 phiên giao dịch
- Risk/Reward **>= 2**
- không có red flag nghiêm trọng
- dữ liệu đủ để kiểm chứng
- Market Regime không phủ định thesis

**Tối đa 3 mã. Không hạ chuẩn để đủ 3 mã. 0 mã là kết quả hoàn toàn hợp lệ.**

### Watch thresholds
Dùng nhất quán:
- **80+**: chỉ High-Conviction nếu toàn bộ gates cùng đạt
- **77–79.9**: Watch #1 / sát ngưỡng
- **73–76.9**: Watch
- **<73**: Reject hoặc theo dõi xa
- Red Flag: loại khỏi long scanner cho tới khi red flag được giải quyết

Không làm tròn 79.x lên 80.

---

## 5. Các lớp phân tích bắt buộc

Mỗi lần scan phải xem xét đủ các lớp sau.

### A. Market Regime
Đánh giá:
- VN-Index, HNX-Index, UPCoM-Index
- breadth
- volume/liquidity
- vùng support/resistance
- MA/MACD/RSI/Stochastic khi hữu ích
- Wyckoff phase
- SMC structure: BOS/CHOCH/liquidity sweep/order block nếu có căn cứ
- Risk-On / Neutral / Risk-Off

Market Regime có quyền **veto** một setup đẹp.

### B. Vĩ mô Việt Nam
Theo dõi khi có dữ liệu mới:
- GDP/IIP/PMI
- CPI/core inflation
- tỷ giá USD/VND
- lãi suất/liquidity liên ngân hàng
- tín dụng
- FDI
- chính sách tài khóa/tiền tệ
- nâng hạng/chỉ số chỉ khi còn là catalyst thực, không mặc định bullish

### C. Global macro
Tối thiểu:
- DXY
- US Treasury yields
- Fed expectations
- dầu/commodity nếu liên quan
- thị trường Mỹ/châu Á
- geopolitical risk

### D. Sector rotation + Relative Strength
Xác định:
- ngành dẫn dắt;
- ngành mất leadership;
- mã outperform khi market yếu;
- mã underperform dù catalyst ngành tốt.

**Catalyst tốt nhưng stock không phản ứng = anti-confirmation.**

### E. Fundamental
Không chỉ dùng target 12 tháng.
Xem:
- tăng trưởng doanh thu/lợi nhuận;
- biên lợi nhuận;
- chất lượng lợi nhuận/cash flow;
- leverage;
- valuation;
- earnings revision;
- dilution/corporate action;
- legal/accounting risk.

**Target 12M không được dùng để suy ra xác suất +5%/7D.**

### F. Catalyst
Phân loại:
- Confirmed
- High Probability
- Speculative

Đánh giá:
- timing có nằm trong 7 phiên không;
- đã price-in bao nhiêu;
- catalyst có binary/geopolitical risk không;
- có thể đảo chiều nhanh không.

### G. Technical + Volume/Price
Đánh giá:
- trend/structure;
- breakout/retest;
- support/resistance;
- volume expansion/contraction;
- absorption/distribution;
- failed breakout/upthrust/spring;
- gap/corporate action adjustment.

Breakout không có follow-through/volume/flow = giảm confidence.

### H. Money Flow
Nếu có dữ liệu:
- foreign;
- tự doanh;
- tổ chức trong nước;
- ETF/index mechanical flow;
- retail/crowd.

Phải phân biệt:
- discretionary accumulation
- mechanical rebalance
- speculative crowd flow

### I. Crowd Sentiment + Price-In
Theo dõi:
- báo chí;
- diễn đàn/mạng xã hội khi có dữ liệu;
- FOMO;
- panic/capitulation;
- crowded trade.

Không dùng sentiment mạng xã hội như nguồn sự thật fundamental.

### J. Risk/Reward + Bear Case
Phải có:
- entry/reference;
- target >= +5%;
- invalidation/stop logic;
- R/R;
- bear case mạnh nhất;
- red flags.

---

## 6. High-Conviction Score v1.0

Đây là rubric vận hành để Agent chấm nhất quán. Tổng 100 điểm:

| Nhóm | Điểm tối đa |
|---|---:|
| Market Regime + VN macro + global fit | 15 |
| Sector rotation + relative strength | 10 |
| Fundamental quality | 10 |
| Catalyst quality + timing | 10 |
| Technical structure | 10 |
| Volume/price + Wyckoff/SMC | 15 |
| Foreign/self-trading/institutional flow | 10 |
| Crowd sentiment + price-in | 5 |
| Risk/Reward | 10 |
| Bear case/red-flag cleanliness | 5 |
| **Tổng** | **100** |

### Penalty bắt buộc
Có thể trừ thêm nếu:
- expansion/FOMO: -3 đến -10
- catalyst đã price-in mạnh: -3 đến -8
- foreign/institutional divergence: -2 đến -8
- market regime Risk-Off: -5 đến -15
- corporate action chưa adjusted: **không chấm cho tới khi adjusted**
- liquidity quá thấp/manipulation risk: -5 đến -15
- dilution/legal/accounting red flag: -5 đến -20

Score chỉ là một lớp. **Gates ở mục 4 vẫn phải đạt độc lập.**

---

## 7. Estimated Confidence

Estimated Confidence là **ước lượng có calibration**, không phải xác suất thống kê được bảo đảm.

Chỉ cho **>80%** khi có convergence rõ giữa:
1. price/technical;
2. volume/flow;
3. catalyst/fundamental;
4. market/sector regime;
5. R/R.

Giảm confidence khi:
- market regime ngược chiều;
- setup phụ thuộc một headline/geopolitical event;
- breakout gần resistance nhưng follow-through yếu;
- foreign và tự doanh xung đột;
- volume giảm sau breakout;
- ETF flow có thể chỉ là mechanical;
- crowd quá hưng phấn;
- nguồn dữ liệu chưa hoàn chỉnh.

Không “làm tròn” 79–80% thành >80%.

---

## 8. Anti-confirmation bias — bắt buộc

Trước khi chọn một mã, Agent phải trả lời ít nhất 3 câu:

1. **Bằng chứng mạnh nhất chống lại thesis là gì?**
2. **Nếu thesis sai, dấu hiệu nào sẽ xuất hiện trước?**
3. **Có dữ liệu nào đang bị cherry-pick vì phù hợp với quan điểm hiện tại không?**

Nếu không tìm được bear evidence, phải chủ động tìm lại nguồn/dữ liệu thay vì mặc định thesis đúng.

Không giữ một mã ở #1 chỉ vì scanner hôm trước đã thích nó.

---

## 9. Corporate action

Trước khi TA:
- kiểm tra cổ tức cổ phiếu;
- stock split;
- quyền mua;
- thưởng cổ phiếu;
- ngày GDKHQ;
- thay đổi số lượng cổ phiếu.

Nếu có corporate action:
- dùng adjusted price;
- ghi rõ event;
- không coi raw-price gap là crash/breakout.

---

## 10. Prediction ledger và chấm WIN/LOSS

Mỗi prediction mới phải được append vào:
`/data/scanner/predictions.csv`

Các trường tối thiểu:
- prediction_id
- issue_date
- ticker
- exchange
- reference_price
- target_price
- win_threshold_pct
- horizon_sessions
- deadline_session
- hc_score
- estimated_confidence_pct
- rr
- market_regime
- status
- mfe_pct
- mae_pct
- outcome
- lesson

### Rule hiện hành
Đối với prediction phát hành theo skill v1:
- **WIN** nếu giá chạm tối thiểu **+5%** so với reference trong cửa sổ 7 phiên;
- **LOSS** nếu không chạm;
- có thể WIN bằng intraday high nếu nguồn giá xác nhận target đã được chạm;
- không cần đóng cửa trên target để WIN, trừ khi prediction ban đầu quy định khác.

### Không hồi tố
- không đổi target;
- không đổi reference;
- không kéo dài deadline;
- không đổi ngưỡng sau khi prediction đã phát hành;
- prediction cũ dùng đúng rule/version lúc phát hành.

### Calibration report
Trước prediction mới, nếu có prediction đủ hạn:
- cập nhật WIN/LOSS;
- completed n;
- hit rate;
- average MFE/MAE nếu đủ dữ liệu;
- lesson;
- kiểm tra overconfidence.

Sample nhỏ phải ghi rõ, ví dụ `n=1` không đủ để suy ra độ chính xác dài hạn.

---

## 11. Data-source hierarchy

Ưu tiên theo thứ tự:

1. **Nguồn chính thức**: HOSE/HNX/UPCoM, công bố doanh nghiệp, IR, SSC, GSO/SBV, FTSE/MSCI nếu liên quan.
2. **Dữ liệu thị trường đáng tin cậy**: bảng giá/market data có timestamp.
3. **Báo cáo CTCK**: dùng cho estimate/valuation, luôn ghi horizon.
4. **Báo chí tài chính uy tín**.
5. **Community/social**: chỉ dùng cho crowd sentiment, không dùng như fact chính.

Với claim quan trọng:
- ưu tiên 1 primary source;
- hoặc >=2 nguồn độc lập nếu primary chưa có;
- nếu dữ liệu mâu thuẫn, nói rõ và không giả định.

---

## 12. Output chuẩn cho scan sau phiên

Thứ tự bắt buộc:

1. **Kết luận một dòng**: số mã High-Conviction + có/không phát prediction.
2. **Market Regime** + lý do.
3. **Macro/global** ngắn gọn.
4. **Sector rotation / money flow**.
5. **Candidate analysis** từ tốt nhất xuống.
6. **Ranking table**:
   - ticker
   - HC Score
   - Estimated Confidence
   - expected upside
   - R/R
   - verdict
7. **Track record & calibration**.
8. **Trigger cho phiên kế tiếp**.

Nếu 0 mã:
> **High-Conviction = 0. Không hạ chuẩn.**

Không kết luận BUY chỉ vì một mã đứng đầu ranking.

---

## 13. Output chuẩn cho trade plan intraday

Nếu người dùng hỏi “trade hôm nay/chiều nay”:
- đọc portfolio current state;
- kiểm tra market intraday;
- phân loại từng holding: HOLD / REDUCE / EXIT / ADD / NO AVERAGE;
- đưa vùng giá và quantity tham khảo khi có đủ dữ liệu;
- dùng LO ưu tiên hơn mua đuổi;
- định nghĩa điều kiện **cancel**;
- nếu market mất support/regime xấu đi, ưu tiên cash.

Không biến intraday plan thành High-Conviction prediction.

---

## 14. Nguyên tắc quản trị danh mục

- Không dùng giá vốn như lý do duy nhất để giữ/mua/bán.
- Đánh giá expected return/risk từ **thời điểm hiện tại**.
- Theo dõi concentration risk.
- Sau khi cắt mã yếu, không bắt buộc tái đầu tư ngay.
- Cash là một vị thế hợp lệ.
- Không bình quân giá xuống nếu thesis chưa được xác nhận.
- Không chase expansion candle khi R/R <2.
- Với turnaround/distress: scale-in nhỏ, đòi hỏi absorption + fundamental confirmation.

---

## 15. Cách gọi skill

Ví dụ:
- `$chungkhoan quét sau phiên hôm nay`
- `$chungkhoan đánh giá GVR 7 phiên tới`
- `$chungkhoan lập chiến lược trade chiều nay theo danh mục hiện tại`
- `$chungkhoan cập nhật track record và scan mới`

Nếu Agent không hỗ trợ cú pháp `$skill`, vẫn phải đọc file này và thực hiện cùng logic.

---

## 16. Definition of Done

Một run hoàn chỉnh chỉ được coi là xong khi:
- dữ liệu ngày/giờ được xác nhận;
- EOD/intraday được phân biệt;
- Market Regime được chấm;
- đủ các lớp bằng chứng;
- anti-confirmation được thực hiện;
- candidate không bị làm tròn để qua ngưỡng;
- track record cũ đã đủ hạn được cập nhật trước prediction mới;
- output có nguồn kiểm chứng;
- nếu prediction mới được phát hành, ledger được cập nhật.
