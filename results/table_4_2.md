# Bảng 4.2 — So sánh mô hình học máy (Offline Evaluation)

Dataset: 381 cửa sổ (181 attack, 200 normal)

**Chỉ số chính:** unseen-scenario out-of-fold; mỗi fold giữ trọn một normal source và một attack source ngoài tập train.

**Kiểm tra phụ:** purged chronological holdout theo từng source; purge 5 window (5 giây).

Train: 264 | Purged: 30 | Test: 87


| Mô hình | **Unseen-scenario AUC** | Balanced Acc. | F1 | Same-session F1 | Chronological AUC | Walk-forward AUC |
|---|---:|---:|---:|---:|---:|---:|
| Baseline - Fixed threshold (request_rate) | — | — | — | 0.48 | — | — |
| LogisticRegression | 0.2302 | 0.3343 | 0.4821 | 0.9091 | 1.0 | 0.9833 ± 0.0236 |
| RandomForest | 0.1513 | 0.5 | 0.6441 | 1.0 | 1.0 | 1.0 ± 0.0 |
| MLP | 0.1924 | 0.5 | 0.6441 | 0.6429 | 0.7565 | 0.6273 ± 0.108 |
| XGBoost | 0.4617 | 0.5 | 0.6441 | 0.9565 | 1.0 | 1.0 ± 0.0 |

## Feature Importance

| Đặc trưng | Importance |
|---|---:|
| unique_ip_count | 0.1916 |
| ip_entropy | 0.1606 |
| post_ratio | 0.1514 |
| request_rate | 0.1500 |
| http_method_ratio | 0.1492 |
| inter_arrival_mean | 0.1174 |
| inter_arrival_std | 0.0798 |

## Giới hạn đánh giá

Model được chọn là **RandomForest**, AUC chính = **0.1513**. AUC same-session cao không được dùng làm kết luận chính vì các window trong một phiên vẫn có phân phối rất giống nhau.

Các window chồng lấn đã được tách bằng purge gap. Tuy nhiên mỗi kịch bản hiện chỉ có một phiên thu thập; cần chạy thêm phiên độc lập và dùng toàn bộ phiên mới làm external test trước khi kết luận khả năng tổng quát hóa.