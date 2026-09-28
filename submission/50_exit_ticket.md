# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling
đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy tắc riêng? Vì sao?

Đây cần một quy tắc riêng về seam/cross-camera, không nên tự động coi là `DUPLICATE`. `DUPLICATE` phù hợp với trường hợp một physical object bị gán nhiều box trong cùng annotation space. Ở seam, cùng một object có thể được nhìn thấy đồng thời bởi hai camera nên cần xác định policy output trước khi ghép. Trước khi merge hoặc nối track cần có timestamp, calibration giữa hai camera và evidence cho thấy hai box thực sự là cùng một physical object. Nếu chưa đủ evidence thì giữ hai box riêng và đưa vào adjudication.

2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera.

Trên cùng camera, giữ cùng track ID khi vẫn xác định đó là cùng một physical object, kể cả khi bị occlusion ngắn; bbox tại frame bị che chỉ bao phần nhìn thấy và dùng trạng thái `Occluded`. Theo hướng dẫn CVAT của lab, nếu object xuất hiện lại trong dưới 25 frame thì giữ ID cũ. `Outside` dùng khi object thực sự không còn bbox trong frame đó; nếu object đã ra khỏi khung và quay lại sau đó thì tạo track mới. Thêm keyframe khi interpolation không còn bám đúng geometry, ví dụ khi bbox bị drift hoặc hình dạng/vị trí thay đổi đáng kể.

Trước khi nối track qua hai camera cần ít nhất timestamp đồng bộ, calibration/camera mapping, evidence về cùng physical object và policy xác định cách duy trì identity giữa camera. Không nối chỉ dựa vào số ID hoặc việc hai box có hình dáng giống nhau.

3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`), bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm?

Ở `adasind_019560.jpg`, object `L7`, ban đầu tôi cho rằng box `Pedestrian` là hợp lý. Sau khi mở reference và compare, `L7` được xác định là `SPURIOUS` vì người này đang cưỡi xe hai bánh và đã được bao trong một box `Bike`; theo R03 không cần thêm `Pedestrian`.

Tôi không sửa trực tiếp file đã lock. Tôi ghi finding vào `findings.csv` với `rule_id=R03`, phân loại P1 và đưa case vào rework. Từ case này tôi bổ sung guideline patch để self-QC có bước kiểm tra riêng các trường hợp người và xe hai bánh nằm gần nhau.

Nếu làm lại slice, tôi sẽ kiểm tra rider/Bike trước khi khóa annotation và đặc biệt rà lại các trường hợp có khả năng xuất hiện đồng thời `Pedestrian` và `Bike`, thay vì chỉ kiểm tra từng box độc lập.