# 1. THÊM SUBMODULE
- Truy cập Codespaces Github
```
cd ~/RPLIDAR_A3M1
git submodule add -b kirkstone https://git.yoctoproject.org/poky poky
git submodule add -b kirkstone https://github.com/openembedded/meta-openembedded.git meta-openembedded
git submodule add -b kirkstone https://github.com/agherzan/meta-raspberrypi.git meta-raspberrypi
git submodule add -b kirkstone https://github.com/ros/meta-ros.git meta-ros
git submodule status
git add .
git commit -m "Add Yocto kirkstone submodules"
git push origin main
```
- Tại Laptop
```
git clone https://github.com/vxtruog/RPLIDAR_A3M1.git
cd ~/RPLIDAR_A3M1
git submodule status
git submodule init
git submodule update
```

# 2. XÂY DỰNG MÔI TRƯỜNG ROS2 HUMBLE VỚI YOCTO PROJECT TẠI LAPTOP
- Xây dựng môi trường ROS2 tại laptop
```
sudo apt install gfortran
cd ~/../poky
source oe-init-build-env
cd ../..
./vuxuantruong.sh
```

