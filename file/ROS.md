# ROS

## 安装 rviz-visual-tools

```bash
sudo apt-get install ros-melodic-rviz-visual-tools
```

github 链接：[rviz-visual-tools](https://github.com/PickNikRobotics/rviz_visual_tools)



## 播放 rosbag 并在 RVIZ 中显示

```bash
# 运行 roscore
roscore

# 播放 rosbag
rosbag play XXX.bag -l

# 打开 rviz，点击 Add 添加消息类型，以 点云(PointCloud2) 为例
rviz

# 需要输入 Pointloud2 的 topic 以及 Fixed Frame
# 查看 Pointloud2 的 topic 
rosbag info XXX.bag  #(在底部显示)

# 查看 Fixed Frame
rostopic echo topic(Pointloud2 的 topic ) | grep frame_id
```



## jsk_recognition_msgs/BoundingBoxArray.msg：没有那个文件或目录

编译出错：`fatal error: jsk_recognition_msgs/BoundingBoxArray.h: 没有那个文件或目录`

出错原因：重新安装 ros 之后，部分功能未安装

解决方法：

```bash
sudo apt-get install ros-melodic-jsk-recognition-msgs & sudo apt-get install ros-melodic-jsk-rviz-plugins
```

总结：没有消息类型可以使用 `sudo apt-get install ros-melodic-XXX` 进行安装，后面的安装语句不是所有的消息类型都有 rviz 插件。

## Could not find a package configuration file provided by "aruco_ros" with any of the following names:

```bash
EIGEN3_INCLUDE_DIR MEKF: /usr/include/eigen3
-- Could NOT find aruco_ros (missing: aruco_ros_DIR)
-- Could not find the required component 'aruco_ros'. The following CMake error indicates that you either need to install the package with the same name or change your environment so that it can be found.
CMake Error at /opt/ros/melodic/share/catkin/cmake/catkinConfig.cmake:83 (find_package):
  Could not find a package configuration file provided by "aruco_ros" with
  any of the following names:

    aruco_rosConfig.cmake
    aruco_ros-config.cmake

  Add the installation prefix of "aruco_ros" to CMAKE_PREFIX_PATH or set
  "aruco_ros_DIR" to a directory containing one of the above files.  If
  "aruco_ros" provides a separate development package or SDK, be sure it has
  been installed.
```

解决方法：

```bash
sudo apt-get install ros-melodic-aruco-ros
```

