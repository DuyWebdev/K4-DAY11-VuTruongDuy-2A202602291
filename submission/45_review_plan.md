# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `adasind_271039.jpg` / center + mid | Nhiều ca `SPURIOUS`, `MISSING`, gồm `L_only`, `LM_noR`, `RM_noL`, `R_only`, `M_only` | Có nhiều discrepancy giữa L/R/M và tập trung ở center/mid, nên cần kiểm tra lại phạm vi đối tượng, class và geometry trước khi kết luận nguyên nhân | `findings.csv`, `model_compare.md`, `iou_sweep.md`, ảnh frame và overlay nếu có |
| `adasind_295948.jpg` / center + mid | `SPURIOUS`, `MISSING`, `WRONG_CLASS`, `IGNORE_SCOPE` | Có nhiều loại discrepancy khác nhau trên cùng frame, phù hợp để kiểm tra riêng class mapping, ignore_region và phạm vi box | `findings.csv`, `model_compare.md`, `zone_table.md`, ảnh frame và overlay nếu có |

Giới hạn của kết luận từ ba frame ADASIND: đây chỉ là quan sát trên ba frame của một camera và một lát cắt được giao, không đủ để ước lượng tỷ lệ lỗi của toàn bộ dataset hoặc kết luận rằng một loại lỗi có tính đại diện cho toàn bộ hệ thống. Các discrepancy giữa L/R/M cũng không mặc nhiên là lỗi annotation; cần đối chiếu ảnh gốc, rule và evidence trước khi rework.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh
như nhiều ca độc lập), và vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi: kiểm tra đủ 8 tổ hợp `front/rear/left/right × normal/hard`, tổng cộng 200 frame theo kế hoạch sampling. Khi review, ghi nhận camera, điều kiện `normal/hard`, scene/cảnh và frame; tránh coi các frame liên tiếp trong cùng một cảnh là các ca độc lập để không làm lệch độ phủ. Các frame được chọn nhằm phát hiện và ưu tiên những trường hợp cần soi kỹ như missing, spurious, wrong class, geometry hoặc ignore_region. Đây là kế hoạch sampling có mục tiêu nên không phải mẫu ngẫu nhiên đại diện cho toàn bộ dữ liệu; vì vậy kết quả review không được dùng trực tiếp để tính tỷ lệ lỗi của toàn dataset.