# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `5b46395baa5c066d59b4233179ac93c0e19acf6a8c5c7503419d58c7c6e69612`; slice `B4-edge`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_236370.jpg, adasind_258420.jpg, adasind_310008.jpg. Frame thiếu trong export: không.
TP=14; FP=3; FN=6; số lần đối chiếu=22; mean IoU của TP=0.874.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.636 | 0.918 | 0.818 |
| precision | 0.824 | 0.860 | 0.500 |
| recall | 0.700 | 0.678 | 0.250 |
| jaccard | 0.609 | 0.635 | 0.200 |
| dice | 0.757 | 0.740 | 0.333 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 1 | 1 | 3 | 0.818 | 0.500 | 0.250 | 0.200 | 0.333 |
| Car | 1 | 0 | 1 | 0.955 | 1.000 | 0.500 | 0.500 | 0.667 |
| Pedestrian | 8 | 2 | 1 | 0.864 | 0.800 | 0.889 | 0.727 | 0.842 |
| ThreeWheeler | 3 | 0 | 1 | 0.955 | 1.000 | 0.750 | 0.750 | 0.857 |
| Truck | 1 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_236370.jpg | 6 | 1 | 1 | 0.750 | 0.857 | 0.857 |
| adasind_258420.jpg | 3 | 2 | 5 | 0.333 | 0.600 | 0.375 |
| adasind_310008.jpg | 5 | 0 | 0 | 1.000 | 1.000 | 1.000 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Car | Pedestrian | ThreeWheeler | Truck | <missing> |
|---|---:|---:|---:|---:|---:|---:|
| Bike | 1 | 0 | 1 | 0 | 0 | 2 |
| Car | 0 | 1 | 0 | 0 | 0 | 1 |
| Pedestrian | 0 | 0 | 8 | 0 | 0 | 1 |
| ThreeWheeler | 0 | 0 | 0 | 3 | 0 | 1 |
| Truck | 0 | 0 | 0 | 0 | 1 | 0 |
| <extra> | 1 | 0 | 1 | 0 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
