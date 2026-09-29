# Escalation ticket

## Ticket 1

- **Frame:** adasind_258420.jpg — object_ref L5+R8 (LR_noM, vùng mid)
- **Ảnh chụp:** submission/screenshots/escalation_258420_L5R8.png
- **Expected impact:** Box có trong L và R nhưng model (YOLO26m) không phát hiện được; nếu đây là pattern lặp lại trên nhiều frame edge/mid, model cần được fine-tune thêm data fisheye để giảm false negative ở vùng biến dạng cao. Ảnh hưởng ước tính: tăng FN ~15% ở vùng mid nếu không xử lý.
- **Owner:** ai_team
- **Recommendation:** Thu thập thêm hard case fisheye vùng mid cho training set; xem xét augment với perspective distortion; gắn cờ E2_guideline_gap để guideline team bổ sung hướng dẫn attribute edge_zone bằng overlay thay vì ngưỡng số thuần túy.

## Ticket 2

- **Frame:** adasind_258420.jpg — M3, M4, M5, M6, M7, M8, M11 (M_only, vùng mid)
- **Ảnh chụp:** submission/screenshots/escalation_258420_Monly.png
- **Expected impact:** Model sinh 7 box thừa trên một frame duy nhất ở vùng mid; false positive rate cao ở vùng fisheye biến dạng sẽ làm tăng thời gian review thủ công và giảm precision tổng thể của pipeline.
- **Owner:** ai_team
- **Recommendation:** Phân tích cluster M_only theo zone để xác định pattern false positive; cân nhắc post-processing NMS thêm hoặc confidence threshold cao hơn cho vùng mid fisheye.
