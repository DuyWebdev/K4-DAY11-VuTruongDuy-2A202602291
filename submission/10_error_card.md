## Phân tích của bạn

Lỗi nổi bật là nhóm sai lệch giữa annotation L và reference/model M ở các vùng center/mid, trong đó có các trường hợp SPURIOUS và MISSING được ghi nhận trong findings. Một ví dụ cụ thể là `adasind_271039.jpg`, với các object_ref `L1`, `L5+M5`, `L7+M8` và `L8` được ghi nhận là SPURIOUS; đồng thời `R4+M4`, `R5`, `R6`, `R7+M6`, `R9`, `R10` được ghi nhận là MISSING.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: Các sai lệch này có thể đến từ khác biệt về phạm vi đối tượng được gán nhãn, vị trí/geometry của box hoặc cách xác định đối tượng trong ảnh fisheye. Evidence hiện có cho thấy discrepancy tập trung ở các cell `L_only`, `LM_noR`, `RM_noL`, `R_only` và `M_only`; vì vậy chưa đủ cơ sở để kết luận tất cả đều là lỗi annotation hay lỗi reference/model.

- Cách sửa và ai nhận việc (`owner`): Annotator kiểm tra lại các trường hợp discrepancy trực tiếp trên ảnh fisheye gốc và đối chiếu R01–R09 trước khi sửa. Chỉ rework những trường hợp xác nhận là lỗi; các trường hợp chưa đủ bằng chứng được giữ lại để QA/diagnosis tiếp tục xác minh.

- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): `submission/findings.csv`; `submission/r3_diag/model_compare.md`; `submission/r3_diag/iou_sweep.md`; `submission/r3_diag/zone_table.md`. Các case cụ thể gồm `adasind_271039.jpg:L1`, `L5+M5`, `L7+M8`, `L8`, `R4+M4`, `R5`, `R6`, `R7+M6`, `R9`, `R10`. Rules liên quan cần đối chiếu gồm R01–R09.