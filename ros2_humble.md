# 1. Tạo môi trường làm việc với ROS2 trên máy ảo
- Cài máy ảo để chạy trên Windows: Oracle VM VirtualBox.
- Cài hệ điều hành
  + Nếu CPU yếu thì cài Ubuntu 22.04 LTS (hỗ trợ bản ROS2 Humble) => tôi dùng bản này.
  + Nếu CPU khoẻ thì cài Ubuntu 24.04 LTS (hỗ trợ các bản ROS2 mới nhất).
- Lỗi Terminal không mở được
  + Bước 1 -> truy cập Settings.
  + Bước 2 -> chọn Region & Language.
  + Bước 3 -> thay đổi ngôn ngữ khác và Restart.

- Các lệnh tiếp theo trên Terminal để cài ROS2
```
su -
usermod -aG sudo <username>
exit
reboot
```
- Truy cập https://docs.ros.org/ và làm theo hướng dẫn để cài đặt ROS2 phù hợp

- Cài đặt môi trường Python3 để build packages
```
sudo apt-get install python3-pip
sudo apt install python3-colcon-common-extensions
```

- Cài đặt môi trường luôn chạy source khi mở Terminal
```
cd ~/<folder>/
colcon build
gedit ~/.bashrc
  + thêm `source /opt/ros/humble/setup.bash`
  + thêm `source ~/<folder>/install/setup.bash`
  + thêm `source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash
```

# 2. Thiết lập giao tiếp với RPLIDAR A3M1
- Cắm USB của RPLIDAR A3M1 vào laptop.
- Trong VirtualBox, Devices → USB → thêm cổng giao tiếp với lidar.
- Kiểm tra kết nối trong máy ảo và cấp quyền cho cổng giao tiếp với lidar
```
lsusb
ls /dev/ttyUSB*
ls -l /dev/ttyUSB0
sudo usermod -aG dialout $USER
sudo reboot
```
https://mickey-happygolucky.hatenablog.com/entry/2024/09/27/230200
https://yiyi-ll.github.io/2025/06/30/yocto%E7%BC%96%E8%AF%91ros2/#1-Yocto%E7%BC%96%E8%AF%91ROS2
