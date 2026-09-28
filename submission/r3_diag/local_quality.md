# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `7175b6ba41856af1a698bd26de67fea1225f1a75923c7f34ffac9114500a38e3`; slice `B4-center`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_270517.jpg, adasind_271039.jpg, adasind_295948.jpg. Frame thiếu trong export: không.
TP=12; FP=6; FN=8; số lần đối chiếu=23; mean IoU của TP=0.860.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.522 | 0.878 | 0.696 |
| precision | 0.667 | 0.733 | 0.500 |
| recall | 0.600 | 0.668 | 0.500 |
| jaccard | 0.462 | 0.506 | 0.364 |
| dice | 0.632 | 0.664 | 0.533 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 2 | 0 | 1 | 0.957 | 1.000 | 0.667 | 0.667 | 0.800 |
| Car | 3 | 0 | 2 | 0.913 | 1.000 | 0.600 | 0.600 | 0.750 |
| Pedestrian | 4 | 4 | 3 | 0.696 | 0.500 | 0.571 | 0.364 | 0.533 |
| ThreeWheeler | 2 | 1 | 2 | 0.870 | 0.667 | 0.500 | 0.400 | 0.571 |
| Truck | 1 | 1 | 0 | 0.957 | 0.500 | 1.000 | 0.500 | 0.667 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_270517.jpg | 7 | 0 | 0 | 1.000 | 1.000 | 1.000 |
| adasind_271039.jpg | 4 | 4 | 6 | 0.308 | 0.500 | 0.400 |
| adasind_295948.jpg | 1 | 2 | 2 | 0.333 | 0.333 | 0.333 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Car | Pedestrian | ThreeWheeler | Truck | <missing> |
|---|---:|---:|---:|---:|---:|---:|
| Bike | 2 | 0 | 1 | 0 | 0 | 0 |
| Car | 0 | 3 | 0 | 1 | 1 | 0 |
| Pedestrian | 0 | 0 | 4 | 0 | 0 | 3 |
| ThreeWheeler | 0 | 0 | 0 | 2 | 0 | 2 |
| Truck | 0 | 0 | 0 | 0 | 1 | 0 |
| <extra> | 0 | 0 | 3 | 0 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
