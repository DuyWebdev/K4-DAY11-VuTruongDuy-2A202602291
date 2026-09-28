# Escalation ticket

## Ticket 1

- **Frame:** `adasind_019560.jpg` — `L7`

- - **Ảnh chụp:** `submission/screenshots/c0_L7_spurious.png` — chụp vùng L7 cho thấy box `Pedestrian` dư trong khi rider + xe đã được gộp trong `Bike`.

- **Expected impact:** Có thể tạo nhãn dư `Pedestrian`, làm sai thống kê lớp và gây nhiễu quá trình QA/model training nếu lỗi tương tự lặp lại trên nhiều frame.

- **Owner:** `guideline`

- **Recommendation:** Bổ sung decision check vào R03: nếu người đang cưỡi/điều khiển xe hai bánh thì chỉ dùng một `Bike`; không thêm `Pedestrian`. Chỉ dùng `Pedestrian` + `Bike` riêng khi người đang đi bộ/dắt xe. Áp dụng decision check này trong self-QC trước khi khóa annotation.