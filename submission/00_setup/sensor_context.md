# Sensor context

- Rig: ảnh ADASIND cho thấy một camera fisheye góc rộng quan sát khu vực phía trước/bên hông xe; vị trí gắn camera cụ thể của rig không được cung cấp nên chỉ ghi nhận theo quan sát từ ảnh.
- `ego_body`: ở các frame có thể thấy phần thân/người/phần xe ở vùng sát mép dưới ảnh; riêng `adasind_271039.jpg` không thấy thân xe ego nên không thêm polygon `ego_body`.
- Vòng kính (lens circle): vòng kính fisheye hiện rõ trong cả ba frame, tạo thành vùng ảnh hình tròn lớn ở trung tâm; phần ngoài vòng kính là vùng mép/vành đen cần được xử lý theo `lens_border` đã import.