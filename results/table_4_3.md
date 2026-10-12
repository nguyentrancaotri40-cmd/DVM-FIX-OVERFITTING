# Bảng 4.3 — Hiệu năng Hệ thống Thời gian thực

## 4.3.1 Processing Latency

### Tổng Processing (T3→check_done, mỗi window)

| Metric | Value |
|--------|-------|
| Mean | 7.39 ms |
| P50 (Median) | 8.333 ms |
| P95 | 12.541 ms |
| P99 | 21.125 ms |
| Max | 29.404 ms |

### Chi tiết theo mốc thời gian T1-T6

| Giai đoạn | Ý nghĩa | Mean | P95 |
|-----------|--------|------|-----|
| T1→T2 | Ghi log raw request | 0.1036 ms | 0.9921 ms |
| T3→T4 | Feature Extraction | 0.7781 ms | 3.9024 ms |
| T4→T5 | ML Inference | 6.2169 ms | 8.6062 ms |
| T5→check_done | Alert check | 0.3946 ms | 1.6952 ms |
| T1→T6 | End-to-End | 4.9769 s | 5.012 s (max) |

## 4.3.2 Detection Delay

| Kịch bản tấn công | Delay (s) | Phát hiện? |
|-------------------|-----------|------------|
| get_flood_c200_start | 2.28 | ✅ Có |
| bot_mimicry_start | 5.05 | ✅ Có |

## 4.3.3 Resource Usage

| Metric | Value |
|--------|-------|
| CPU mean | 22.79% |
| CPU max | 100.0% |
| CPU P95 | 96.9% |
| RAM mean | 193.91 MB |
| RAM max | 204.88 MB |