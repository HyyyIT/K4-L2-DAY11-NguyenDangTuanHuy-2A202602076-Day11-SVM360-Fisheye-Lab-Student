# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B4 | MISSING | 2 |
| center | B4 | SPURIOUS | 2 |
| center | C0 | MISSING | 1 |
| center | C0 | SPURIOUS | 2 |
| edge | B4 | MISSING | 2 |
| edge | B4 | SPURIOUS | 1 |
| mid | B3 | BOX_GEOMETRY | 1 |
| mid | B4 | MISSING | 9 |
| mid | B4 | SPURIOUS | 11 |
| unknown | B4 | ATTRIBUTE | 1 |
| unknown | B4 | STRUCTURE | 1 |

## Top defects
- SPURIOUS: 16 (ví dụ frame adasind_019560.jpg)
- MISSING: 14 (ví dụ frame adasind_019560.jpg)
- BOX_GEOMETRY: 1 (ví dụ frame adasind_167700.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: Lỗi nổi bật nhất là SPURIOUS (16 ca) và MISSING (14 ca), tập trung ở vùng mid của frame `adasind_258420.jpg`. Nguyên nhân chính là `E1_annotator_error` — cụ thể là vi phạm R03 (rider split case): tôi tách `Pedestrian` và `Bike` thành hai box riêng thay vì gộp một box `Bike` bao trọn cả người và xe (adasind_236370 L1, adasind_258420 L1+L3). Ngoài ra bỏ sót hệ thống các box Bike trong frame đông đúc (5 MISSING ở adasind_258420). Các M_only (11 ca) chủ yếu là `E4_model_domain` — model YOLOv26m false positive do biến dạng fisheye vùng mid. Lỗi ATTRIBUTE (edge_zone=false sai) là `E2_guideline_gap` — guideline không có visual aid để annotator tự đo r/R trong khi vẽ.
- Cách sửa và ai nhận việc (`owner`): (1) Annotator rework box L1 adasind_236370 và L1+L3 adasind_258420 theo R03 — gộp thành box Bike; (2) Annotator bổ sung box Bike bị bỏ sót (R1, R3, R5, R7 của adasind_258420); (3) Annotator sửa attribute edge_zone=true cho 5 box ở adasind_258420 và adasind_310008; (4) Guideline team bổ sung visual overlay minh họa ngưỡng r/R vào R10; (5) AI team điều tra pattern M_only của YOLO26m ở vùng mid fisheye.
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): screenshots/escalation_258420_L5R8.png cho thấy box L và R nhất quán nhưng model bỏ sót; screenshots/escalation_258420_Monly.png cho thấy 7 box M_only trong vùng mid không có trong L và R. Findings.csv dòng 12–18 (r3_diag adasind_258420) và dòng 12 (r3_diag adasind_236370 L1 L_only R03). Rule R03 và R10 trong docs/02-rules-vi.md.
