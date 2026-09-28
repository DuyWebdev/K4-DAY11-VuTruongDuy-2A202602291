# Guideline patch

- **Rule mới đề xuất:** Khi gặp người đứng/ngồi gần xe hai bánh, phải xác định trạng thái tương tác trước khi gán nhãn: nếu người đang cưỡi/điều khiển xe thì gộp người + xe thành một `Bike`; không thêm `Pedestrian`. Chỉ gán `Pedestrian` và `Bike` riêng khi người đang đi bộ/dắt xe. Trước khi khóa annotation, kiểm tra lại các trường hợp có nguy cơ bị gán đồng thời `Pedestrian` và `Bike`.

- **Áp dụng cho:** `Bike`, `Pedestrian`; đặc biệt các đối tượng ở vùng center/mid/edge có người và xe hai bánh xuất hiện gần nhau.

- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** R03 đã quy định rider + two-wheeler = một `Bike` và người đi bộ/dắt xe = `Pedestrian` + `Bike`, nhưng chưa đưa ra một bước kiểm tra quyết định rõ ràng cho các trường hợp người và xe nằm gần nhau. Case `adasind_019560.jpg:L7` cho thấy có thể phát sinh thêm box `Pedestrian` dù đã có box `Bike` bao rider + xe.

- **`rules_version` mới:** v1.1.0

- **Hiệu lực từ:** Round tiếp theo sau vòng `r2/rework`; áp dụng trong self-QC trước khi khóa annotation.