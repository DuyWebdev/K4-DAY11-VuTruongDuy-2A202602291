# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.

| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | Đông xe, occlusion, vật thể nhỏ và vùng gần mép ảnh | Nhiều đối tượng chồng lấn, dễ missing/spurious hoặc sai class | Giữ nguyên tọa độ ảnh fisheye của camera front, calibration/version và quy ước ignore_region | Hai người review độc lập, đối chiếu rule và geometry; chỉ đưa vào gold sau khi xử lý disagreement |
| rear | Xe phía sau ở khoảng cách gần/xa, occlusion và mật độ giao thông cao | Kích thước vật thể thay đổi nhanh, dễ bỏ sót hoặc box sai phạm vi | Giữ annotation space của rear, calibration/version và mapping class/ignore_region | Review độc lập + adjudication các disagreement; lưu evidence và phiên bản calibration |
| left | Vật thể sát edge, xe hai bánh và các trường hợp bị che khuất | Fisheye distortion và vùng biên làm geometry khó ổn định, dễ nhầm class | Giữ tọa độ fisheye gốc, calibration left và quy tắc xử lý lens/ignore | Review độc lập theo hard/normal, kiểm tra geometry trên ảnh gốc và adjudicate trước khi chốt |
| right | Vật thể sát edge, xe hai bánh, occlusion và cảnh đông | Distortion và seam với camera khác có thể làm box/class không nhất quán | Giữ annotation space, calibration right và mapping class/ignore_region | Review độc lập, kiểm tra seam/cross-camera và adjudicate các ca không thống nhất |

- Khi nào cần refresh gold set (đổi camera, calibration hoặc rule): **Refresh khi camera hoặc calibration thay đổi, khi mapping/class/rule annotation thay đổi, hoặc khi QA phát hiện pattern lỗi mới có thể ảnh hưởng đến reference. Mỗi lần refresh phải version hóa gold set và lưu lý do/evidence.**

- Một ca seam/cross-camera cần policy và evidence trước khi ghép hai box: **Chỉ ghép hai box khi xác định chúng biểu diễn cùng một physical object, có policy về vùng overlap/seam và có evidence từ hai camera cùng thời điểm hoặc cùng scene. Nếu không đủ evidence thì giữ riêng và ghi nhận case để adjudication, không tự động merge.**

- Vì sao peer agreement hoặc quality report trên ảnh một camera chưa chứng minh gold set đúng cho cả bốn camera: **Agreement trên một camera chỉ cho thấy các reviewer nhất quán trong annotation space và điều kiện của camera đó. Bốn camera có calibration, góc nhìn, distortion, seam và phân bố hard case khác nhau; vì vậy cần review riêng theo từng camera và kiểm tra cross-camera trước khi coi tập reference là gold cho toàn hệ thống.**