# Quan sát vạch ô đỗ

- Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh): chọn hai vạch sơn trắng chéo rõ ở phần tiền cảnh của bãi đỗ, mỗi vạch tạo ranh giới giữa các khu vực đỗ xe khác nhau. Các vạch được dừng tại phần sơn còn nhìn thấy, không nối qua phần bị khuất.

- Một vạch/dấu sơn hoặc biên **không** vẽ, và vì sao: không chọn các đường/biên sáng ở khu vực xa và phần mép bãi khi chưa đủ rõ chúng có thực sự tạo ranh giới cho một ô đỗ riêng lẻ. Theo rule, không nên coi mọi đường sơn hoặc mép đường là `parking_line`.

- Polygon `free_space` dừng ở đâu; có phần bị che nào không: polygon dừng trên phần mặt đường trống nhìn thấy của lối xe chạy, tránh các vật thể và các đường/vạch không thuộc vùng mặt đường trống. Không ghi nhận phần bị che cần suy đoán trong vùng `free_space` đã chọn.

- Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”): không có.