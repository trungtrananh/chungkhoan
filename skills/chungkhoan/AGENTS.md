# AGENTS.md — Local rules for skill chungkhoan

Áp dụng cho mọi file trong thư mục này.

1. `SKILL.md` là source of truth cho quy trình scan/trade.
2. Không thay đổi các gate cứng (Score 80, Confidence >80%, upside >=5%/7 phiên, R/R >=2) nếu chưa có yêu cầu rõ ràng của người dùng.
3. Mọi thay đổi rule phải:
   - tăng version trong `SKILL.md`;
   - ghi vào `CHANGELOG.md`;
   - đồng bộ `docs/HIGH_CONVICTION_FRAMEWORK.md`.
4. Không sửa prediction cũ để phù hợp rule mới.
5. Output intraday không được ghi thành official prediction.
6. Không xóa anti-confirmation, market-regime penalty hoặc corporate-action adjustment.
7. Nếu thiếu dữ liệu EOD, trả về "chưa đủ dữ liệu" thay vì bịa số.
