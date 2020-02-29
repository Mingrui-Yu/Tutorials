# ROS 基础用法

[ROS-Tutorials](http://wiki.ros.org/ROS/Tutorials)

## ROS Enivronment 配置

在 ~/.bashrc 中添加 ROS environment setup，该方法会永久有效（个人推荐，否则太麻烦了）
```
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
如果只想对于当前 Terminal 有效，则：
```
source /opt/ros/melodic/setup.bash
```

## 建立 ROS Workspace
example: ~/catkin_ws 为 Workspace 目录
```
mkdir -p ~/catkin_ws/src 
cd ~/catkin_ws/
catkin_make    # 首次会创建 CMakeLists.txt，之后类似于 cmake
```
注：-p 的意义为：可以创建目录及其子目录，否则只能创建到一级目录 catkin_ws

如果想使用该 Workspace，需要在 Workspace 目录的终端中：
```
source devel/setup.bash  # 只对当前终端有效
```

## ROS 文件操作方法
```
rospack find [package_name]

roscd [locationname[/subdir]]

rosls [locationname[/subdir]]
```

##  Package
### 创建：
```
cd ~/catkin_ws/src

# 创建 beginner_tutorials 文件夹其中包括 package.xml & CMakeLists.txt
# catkin_create_pkg <package_name> [depend1] [depend2] [depend3]
catkin_create_pkg beginner_tutorials std_msgs rospy roscpp
```
### Build：
```
cd ~/catkin_ws
catkin_make
```


## Run ROS
首先，必须，总领全局：
```
roscore
```
新的终端：
```
# optional
rosnode list  # 查看当前的 nodes 列表
rosnode info [nodename] # 查看 nodename 的具体信息
```
### rosrun
新的终端：
```
# rosrun [package_name] [node_name]
rosrun turtlesim turtlesim_node  # 小乌龟
```

新的终端：
```
rosrun turtlesim turtle_teleop_key  # 键盘方向键输入
```

### Watch the Node/Topic/Message Graph:

新的终端：
```
rosrun rqt_graph rqt_graph
```

### rostopic
```
rostopic echo [topic]   # will show topic's  message
rosmsg show [message]]  #  show message's detals
```

### roslaunch
同时启动多个 nodes

## 使用例子
[Creating a ROS msg and srv](http://wiki.ros.org/ROS/Tutorials/CreatingMsgAndSrv)

[Writing a Simple Publisher and Subscriber (C++)](http://wiki.ros.org/ROS/Tutorials/WritingPublisherSubscriber%28c%2B%2B%29)

[Writing a Simple Service and Client (C++)](http://wiki.ros.org/ROS/Tutorials/WritingServiceClient%28c%2B%2B%29)