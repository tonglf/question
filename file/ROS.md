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



## rviz 点击某个点显示该点的信息

方法一：
		rviz上方有 `Select` 选项，右击，勾选 Selection 选项，在左面项目栏里就有 Selection 的部分了。点击上方的  `Select` 选项，再选中点，左侧 Selection 里就会显示该点的信息了，包括：Position（X、Y、Z）、intensity、ring、timestamp。

方法二：
		rostopic list 会显示 /clicked_point，去终端打印该话题的内容：

```bash
rostopic echo /clicked_point
```

点击 rviz 上方的 `Publish Point`，然后再选择点，在刚打开的终端就会显示该点的信息：

```bash
~$ rostopic echo /clicked_point
header: 
  seq: 0
  stamp: 
    secs: 1661916298
    nsecs: 655576318
  frame_id: "base_link"
point: 
  x: 108.888648987
  y: 25.8663330078
  z: 2.0133972168
---

```



## ROS 使用 PCL 出错

在ubuntu18.04上使用ros中的PCL库时会遇到lz4 冲突问题，问题如下：

```bash
error: conflicting declaration ‘typedef struct LZ4_streamDecode_t LZ4_streamDecode_t’
typedef struct { unsigned long long table[LZ4_STREAMDECODESIZE_U64]; } LZ4_streamDecode_t;
```

解决方法如下：

```bash
sudo mv /usr/include/flann/ext/lz4.h /usr/include/flann/ext/lz4.h.bak
sudo mv /usr/include/flann/ext/lz4hc.h /usr/include/flann/ext/lz4.h.bak

sudo ln -s /usr/include/lz4.h /usr/include/flann/ext/lz4.h
sudo ln -s /usr/include/lz4hc.h /usr/include/flann/ext/lz4hc.h
```



## PCL：对 '...' 未定义的引用

 例如：

```bash
对‘pcl::search::Search<pcl::PointXYZ>::getName() const’未定义的引用
```

原因：
	新定义了 PointT 类型，导致使用某些类使用出错。

解决方法：
	添加 宏定义以及 hpp 文件，在 PCL 的官方文档中已经说明过该情况。

```cpp
#define PCL_NO_PRECOMPILE	// 在第一行，添加宏定义
#include <pcl/search/kdtree.h>
#include <pcl/search/impl/kdtree.hpp>	// 添加 hpp 文件

// #include <pcl/impl/instantiate.hpp>		// 若有必要可添加该文件
```

参考链接: [官方文档](https://pcl.readthedocs.io/projects/tutorials/en/master/adding_custom_ptype.html#how-to-add-a-new-pointt-type).



## PCL Assertion `px != 0' failed

原因：智能指针未初始化。

解决：使用前初始化。

## 用 ros 工具从 bag 文件中提取点云和图片

**点云**

```bash
rosrun pcl_ros bag_to_pcd <XXX.bag> <topic> <output_directory>
```

参考博客：[ROS：bag数据包内容提取——雷达点云数据和imu数据](https://blog.csdn.net/m0_48748418/article/details/126004787)

**图片**

```bash
# 如果输出的图片数量与 rosbag info 命令查询得到的数量不符，可以减少 _sec_per_frame 参数的值。
rosrun image_view extract_images _sec_per_frame:=0.01 image:=<topic>

rosbag play XXX.bag
```

参考博客：[利用ROS工具从bag文件中提取图片](http://t.zoukankan.com/arkenstone-p-6676203.html)

## 5.000000000000000000000000000000000000e-01

在编译过程中遇到以下问题:

```bash
eric literal operator 'operator""Q'
   BOOST_DEFINE_MATH_CONSTANT(half, 5.000000000000000000000000000000000000e-01, "5.00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000e-01")
   ```
   
  解决方法:
  
  1.  可能是 由于gcc 版本问题，替换成 5；
  2. 参考博客： [ad_with_lanelet2 编译问题解决](https://blog.csdn.net/qq_35632833/article/details/112923613)  




