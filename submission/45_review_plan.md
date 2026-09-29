# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| adasind_258420.jpg (B4-edge, vùng mid) | 5 MISSING (R_only), 2 SPURIOUS (L_only), 7 M_only | Frame có precision thấp nhất (0.600) và recall thấp nhất (0.375); tập trung hầu hết lỗi của slice; cần xác nhận lại toàn bộ box trước khi rework | compare.html, model_compare.html, qa_overlay.html — cần giữ cả ba để đối chiếu ba nguồn L/R/M |
| adasind_236370.jpg (B4-edge, vùng mid) | 1 SPURIOUS (L1), 1 MISSING (R4+M1) | Ca rider vi phạm R03 được cả QA reviewer và reference xác nhận; cần rework box L1 thành Bike và thêm box Bike cho R4 | compare.html — frame này R/M nhất quán nhau, dễ dùng làm bằng chứng rõ ràng |

Giới hạn của kết luận từ ba frame ADASIND: Ba frame chỉ đại diện cho một slice nhỏ (B4-edge) của một camera duy nhất trong điều kiện ánh sáng và mật độ vật nhất định. Tỷ lệ lỗi tính được (TP=14, FP=3, FN=6, jaccard=0.609) không thể suy rộng cho toàn bộ camera hay điều kiện thời tiết/ánh sáng khác. Đặc biệt, frame `adasind_310008.jpg` có precision/recall hoàn hảo (1.0/1.0) nhưng lại là ngoại lệ, không phải quy luật.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh như nhiều ca độc lập), và vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi: Kế hoạch 200 frame phân bổ theo normal/hard trên bốn camera nhằm tối đa đa dạng tình huống (giao lộ, đêm, occlusion, seam). Tuy nhiên nếu nhiều frame liên tiếp được chọn từ cùng một đoạn video, chúng sẽ rất tương đồng nhau (cùng góc nhìn, cùng vật thể) và không mang thêm thông tin độc lập — inflate số lượng nhưng không tăng độ phủ thật. Kế hoạch này chỉ là sampling plan giúp tìm hard case và phân bổ ngân sách review; không đo được tỷ lệ lỗi tổng thể vì 200/50.000 = 0.4% không đủ đại diện thống kê và thiếu random sampling nghiêm ngặt.
