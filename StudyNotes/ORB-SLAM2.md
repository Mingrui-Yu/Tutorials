# ORB-SLAM2  in ROS

## 编译

参考：[raulmur/ORB_SLAM2](https://github.com/raulmur/ORB_SLAM2#7-ros-examples)

在 ~/.bashrc 中添加 ORB-SLAM2 path 至 ROS_PACKAGE_PATH
```
sudo gedit ~/.bashrc

# 添加
export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:/home/mingrui/Mingrui/SLAMProject/ORB_SLAM2/Examples/ROS
```
**NOTICE:** 
* ${ROS_PACKAGE_PATH}:和/home之间不能有空格。
* 添加的位置要在之前添加的其它的 source 命令之后。


编译：
```
cd /home/mingrui/Mingrui/SLAMProject/ORB_SLAM2
chmod +x build_ros.sh

./build_ros.sh
```
会报错：```DSO missing from command line```

解决：[ERROR while running ./build_ros.sh #535](https://github.com/raulmur/ORB_SLAM2/issues/535)


## 使用电脑自带摄像头跑 ORB-SLAM2
参考：[ubuntu16.04下用笔记本摄像头和ROS编译运行ORB_SLAM2的单目AR例程](https://www.cnblogs.com/feifanrensheng/p/8995836.html)

## Android 手机摄像头 与 PC 实现 ROS 通信
参考：[ ROS实时采集Android的图像和IMU数据
](https://www.cnblogs.com/hitcm/p/5616364.html)

**NOTICE:** 
* ```sudo apt-get install ros-melodic-imu-tools``` 修改 ROS 版本
* PC 的 ip 地址 通过 终端输入 ifconfig 查看
* 必须要 roslauch，否则没有 /camera/image_raw 这个 ROS topic

关于 rvis 界面：
* 如果要实时显示 image，需要 Add - By topic - 添加/camera/image_raw/image
* 如果要显示 imu，则需要 Add - By topic - 添加 imu，且在 Fix Frame 中 将 map 改为 imu

### 保存图片

目前没有找到直接保存的方法，选择写一个 ROS node 来接受图像，再通过 OpenCV 进行显示和保存。与上一部分 Android 配合使用。

cmake 的那堆东西还不太懂，所以选择修改 ORB-SLAM2 的 ros_mono.cc 实现。在 ros_mono.cc 同一目录下写了个 ros_camera_capture.cc。

使用方法：

Terminal 1:
```
roscore
```
手机进入 apk 运行

Terminal 2: 在 Android_Camera-IMU 目录
```
roslaunch android_cam-imu.launch
```
（可以关掉 rvis）

Terminal 3:
```
rosrun ORB_SLAM2 CameraCapture
```
按下 q 保存图像（注意保存的目录 SLAMProject/calibrationImages）

(实验发现家里的网真不好，手机和电脑之间的传输很不稳定，切换成 手机热点就好了)

## 手机摄像头标定
参考： [相机标定](相机标定.md)
使用 OpenCV sample.

新建了一个文件夹 SLAMProject/camera_calibration_opencv，作为标定的工作文件夹。

在 VID5.xml 中添加标定图片的路径。

ORB-SLAM2 中需要的参数有 fx, fy, cx, cy, k1, k2, k3, p1, p2，也就是有径向畸变和切向畸变参数，所以要在 in_VID5.xml 中将 <Calibrate_AssumeZeroTangentialDistortion> 改为0。

编译：
```
cd camera_calibration_opencv
mkdir build
cd build
cmake  ..
make
```
运行：
```
./build/Camera_Calibration  in_VID5.xml
```

参数输出在 out_camera_data.xml 中:
* <camera_matrix type_id="opencv-matrix"> 是相机内参矩阵，顺序为 fx, 0, cx; 0, fy, cy; 0, 0, 1;
* <distortion_coefficients type_id="opencv-matrix"> 就是畸变参数，其顺序为 k1, k2, p1, p2, k3。

之后将标定参数填入 ORB-SLAM2 的自己的 ORB_SLAM2/Examples/Monocular/MI9SE.yaml 中

## 使用手机摄像头跑 ORB-SLAM2
参考：[采集Android手机摄像头运行ORB_SLAM2（ubuntu16.04+ROS kinetic）](https://blog.csdn.net/qq_36122936/article/details/88556428?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task)

Terminal 1:
```
roscore
```
手机进入 apk 运行

Terminal 2: 在 Android_Camera-IMU 目录
```
roslaunch android_cam-imu.launch
```
（可以关掉 rvis）

Terminal 3:
```
rosrun ORB_SLAM2 Mono ~/Mingrui/SLAMProject/ORB_SLAM2/Vocabulary/ORBvoc.txt  ~/Mingrui/SLAMProject/ORB_SLAM2/Examples/Monocular/MI9SE.yaml
```