# 1. Giới thiệu RPLIDAR A3M1
- RPLIDAR A3M1 là máy quét laser 2D 360° (LiDAR), do SLAMTEC phát triển. Thiết bị có khả năng thực hiện tới 16.000 phép đo khoảng cách bằng laser mỗi giây với tốc độ quay cao.
- Phạm vi quét từ 0.2m lên đến 25m, dữ liệu đám mây điểm 2D được tạo ra có thể được sử dụng cho việc lập bản đồ, định vị và mô hình hóa đối tượng/môi trường.
- RPLIDAR A3M1 hỗ trợ hoạt động luân phiên ở hai chế độ: Enhanced Mode và Outdoor Mode.
```
+ Với Enhanced Mode, thiết bị hoạt động với bán kính đo và tốc độ lấy mẫu tối đa nhằm đạt được hiệu suất lập bản đồ tối ưu trong môi trường trong nhà.
+ Với Outdoor Mode, thiết có khả năng chống nhiễu từ ánh sáng ban ngày đáng tin cậy hơn, giúp ngăn thiết bị bị “mù” khi hoạt động trong môi trường ngoài trời.
```
- Tần số quét điển hình của RPLIDAR A3M1 là 10 Hz, và tần số này có thể được điều chỉnh tự do trong phạm vi 5–15 Hz tùy theo yêu cầu cụ thể. Với tần số quét 10 Hz, tốc độ lấy mẫu là 16 kHz và độ phân giải góc là 0,225°.
- Độ phẳng trường quét ±1,5°.
- Bước sóng laser là 775 - 795 nm, công suất tối đa 12mW, độ dài xung 60 - 90 µs.
- Khối lượng 190g.
- Nhiệt độ hoạt động từ 0 đến 40°C.

# 2. Cấu tạo và nguyên lý hoạt động RPLIDAR A3M1
- RPLIDAR A3M1 bao gồm một lõi máy quét khoảng cách và một bộ phận truyền động cơ khí giúp lõi máy quét quay với tốc độ cao.
- Người dùng có thể nhận dữ liệu quét khoảng cách thông qua giao diện giao tiếp của RPLIDAR, đồng thời có thể điều khiển việc khởi động, dừng và tốc độ quay của động cơ thông qua tín hiệu PWM.
- RPLIDAR A3M1 được trang bị hệ thống phát hiện tốc độ quay và thích ứng với tốc độ quay. Hệ thống sẽ tự động điều chỉnh độ phân giải góc theo tốc độ quay thực tế.
- RPLIDAR A3M1 dựa trên nguyên lý đo khoảng cách bằng phương pháp laser triangulation và sử dụng phần cứng thu nhận và xử lý hình ảnh tốc độ cao do SLAMTEC phát triển.
- Trong mỗi quá trình đo khoảng cách, RPLIDAR phát ra tín hiệu laser hồng ngoại đã được điều chế, sau đó tín hiệu laser được phản xạ bởi vật thể cần phát hiện. Tín hiệu phản hồi sau đó được lấy mẫu trong RPLIDAR, và bộ xử lý tín hiệu số (DSP) được tích hợp trong RPLIDAR sẽ bắt đầu xử lý dữ liệu mẫu, sau đó xuất ra giá trị khoảng cách và giá trị góc giữa vật thể và RPLIDAR thông qua giao diện giao tiếp. Khi được dẫn động bởi hệ thống động cơ, lõi máy quét khoảng cách sẽ quay theo chiều kim đồng hồ và thực hiện quét 360° đối với môi trường xung quanh.
- Mỗi dữ liệu của một điểm lấy mẫu chứa các thông tin được trình bày bên dưới đây
```
+ Khoảng cách, đơn vị mm, là giá trị khoảng cách hiện tại đo được giữa lõi quay của RPLIDAR và điểm lấy mẫu.
+ Góc phương vị hiện tại của phép đo, đơn vị °.
+ Cờ đánh dấu bắt đầu một vòng quét mới.
+ Giá trị checksum của dữ liệu phản hồi từ RPLIDAR.
```
- RPLIDAR A3M1 sử dụng hệ tọa độ tay trái (left-handed coordinate system). Hướng chính diện của cảm biến là trục X của hệ tọa độ; gốc tọa độ là tâm quay của lõi máy quét khoảng cách. Góc quay tăng dần theo chiều kim đồng hồ.
- RPLIDAR A3M1 sử dụng nguồn điện một chiều 5V DC riêng biệt để cấp nguồn cho lõi máy quét khoảng cách và hệ thống động cơ. RPLIDAR A3M1 tiêu chuẩn sử dụng đầu nối đực XH2.54-5P.
```
+ Đỏ (VCC): 4.9 - 5.2V, nguồn cấp tổng.
+ Vàng (TX): 0 - 3.5V, ngõ ra UART.
+ Xanh lá (RX): 0 - 3.5V, ngõ vào UART.
+ Đen (GND): 0V, nối đất.
+ Xanh dương (PWM): 3.3V, đầu vào tín hiệu điều khiển động cơ.
```
- Giao diện giao tiếp TTL UART, với tốc độ lựa chọn 112500 bps và 256000 bps, chế độ hoạt động 8N1.
- RPLIDAR A3M1 được tích hợp sẵn bộ điều khiển động cơ có chức năng điều chỉnh tốc độ. Người dùng có thể điều khiển việc khởi động, dừng và tốc độ quay của động cơ thông qua chân MOTOCTL trên giao diện. MOTOCTL có thể được điều khiển bằng tín hiệu PWM với tần số và duty cycle phù hợp. Ở chế độ này, tốc độ quay được quyết định bởi duty cycle của tín hiệu PWM đầu vào.
```
+ Điện áp: 3.3 V
+ Tần số: 25000 Hz, tín hiệu vuông, tại tần số quét 10 Hz.
+ Duty cycle: thay đổi tùy cài đặt, thường là 60% tại tần số quét 10 Hz.
```
# 3. Chú ý
- Bốn vít M3 ở mặt đáy không được gắn ốc dài quá 4 mm, nếu không mô-đun bên trong có thể bị hư hỏng.
- Enhanced Mode được thiết kế cho môi trường trong nhà. Ánh sáng trong nhà thông thường (bao gồm cả trường hợp không có ánh sáng) sẽ không ảnh hưởng đến hiệu suất của RPLIDAR. Ánh sáng mạnh (chẳng hạn như laser công suất cao) sẽ gây hại cho hệ thống quang học của LiDAR và cần được tránh.
- Outdoor Mode, RPLIDAR A3 có thể hoạt động bình thường để phát hiện các vật thể dưới ánh sáng môi trường trực tiếp. Tuy nhiên, khoảng cách đo có thể ngắn hơn khi có ánh sáng mặt trời trực tiếp mạnh, và vẫn cần bảo vệ hệ thống quang học khỏi ánh sáng mặt trời chiếu trực tiếp.

# 4. Ứng dụng
- RPLIDAR A3M1 có thể được sử dụng trong các kịch bản ứng dụng sau:
```
+ Điều hướng và định vị robot.
+ Quét môi trường và tái dựng mô hình 3D.
+ Robot dịch vụ hoặc robot công nghiệp hoạt động trong thời gian dài.
+ Điều hướng và định vị robot phục vụ trong gia đình/robot vệ sinh.
+ Định vị và lập bản đồ đồng thời (SLAM).
+ Định vị và tránh vật cản cho đồ chơi thông minh.
```
