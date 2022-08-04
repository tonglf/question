# question
Record recent problems and their solutions.

## GitHub

### 更换电脑后，git clone 出错

更换电脑后，将个人仓库 clone 到本地时，clone 出错，错误信息：

```bash
SSL certificate problem: unable to get local issuer certificate
```

解决方法：

这个问题是由于没有配置信任的服务器HTTPS验证。默认，cURL 被设为不信任任何 CAs，就是说，它不信任任何服务器验证。
最终使用如下方法解决的只需要执行下面命令就可以解决：

```bash
git config --global http.sslVerify false
```

参考链接：https://www.jianshu.com/p/103735801a2e


### 生成 tokens

在本地远程推送时，有时候需要输入 username 和 password，password 不是登录 github 时的密码，而是 tokens，在哪生成 tokens ？

Settings/Developer settings/Personal access tokens

### 切换分支

```bash
git clone XXX.git

cd DIR

# 查看当前所在分支
git branch

# 列出所有分支
git branch -a

# 切换目标分支
git checkout XXX
```

### 新建分支并上传代码

```bash
# 更新本地代码库
git pull

# 查看所在分支
git branch

# 新建分支
git branch XXX

# 切换分支
git checkout XXX

# 添加代码
git add .
git commit -m "xxx"

# 提交代码到指定分支
git push origin XXX(分支名称)
```



### 删除分支

```bash
git branch -d 分支名
git branch -D 分支名		# 强制删除
```



### git commit 后撤销

```bash
# 撤销 commit，不撤销 add
git reset --soft HEAD^

# 同时撤销 commit 和 add
git reset --hard HEAD^
```



## ubuntu

### 不同软件版本切换

当你在系统上装了某一个软件的很多版本的时候，有时候在用的时候需要选择合适的版本，那就需要进行不同版本之间的切换，（以python为例）：

```bash
# 查找已安装的版本，你需要知道你安装了什么版本
 ls /usr/bin/python*
 
# 将不同的版本加入列表中，最后一个数是优先级
update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1  
update-alternatives --install /usr/bin/python python /usr/bin/python3.6 2 

# 列出已经配置版本
update-alternatives --list python

# 切换系统默认的python版本
sudo update-alternatives --config python 
```

参考链接：[ubuntu 下切换python版本](https://blog.csdn.net/samsu0108/article/details/121220366)

### gcc/g++ 不同版本的切换

**ubuntu 18.04 gcc版本为7, ubuntu 16.04 gcc版本为5, 在18.04上使用gcc5**

```bash
# 查看版本(以 gcc 为例)
gcc --version

# 添加 16.04 源
sudo gedit /etc/apt/sources.list

# 打开文件后，将以下两行内容添加至文件末尾
deb http://dk.archive.ubuntu.com/ubuntu/ xenial main
deb http://dk.archive.ubuntu.com/ubuntu/ xenial universe

# 安装 gcc 5 / g++ 5（注意终端输出，可能有的不能安装，选择终端建议安装的源，实在不行的就不安装）
sudo apt install gcc-5 gcc-5--multilib g++-5 g++-5--multilib

# 使用update-alternatives设置gcc和g++：
# update-alternatives是ubuntu系统中专门维护系统命令链接符的工具，通过它可以很方便的设置系统默认使用哪个命令、哪个软件版本。
# 其中 10 ，20 是优先级数值可以自己设定，--slave能保证gcc和g++保持相同的版本。
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 20 --slave /usr/bin/g++ g++ /usr/bin/g++-5
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 10 --slave /usr/bin/g++ g++ /usr/bin/g++-7

# 使用如下命令选择gcc的版本：
sudo update-alternatives --config gcc

# 终端输出结果如下
# ======================================
有 2 个候选项可用于替换 gcc (提供 /usr/bin/gcc)。

  选择       路径          优先级  状态
------------------------------------------------------------
* 0            /usr/bin/gcc-7   70        自动模式
  1            /usr/bin/gcc-5   50        手动模式
  2            /usr/bin/gcc-7   70        手动模式

要维持当前值[*]请按<回车键>，或者键入选择的编号：
# ======================================

# 验证是否修改成功
gcc -v
```

参考链接：[linux下gcc、g++不同版本的安装和切换](https://www.jianshu.com/p/f66eed3a3a25)

### ubuntu 18.04 python 升级之后，终端打不开

ubuntu 18.04 python 由 3.6 升级到 3.7 之后，终端不能直接打开，需要右键选择在终端打开才行

解决方法：修改文件内容

```bash
sudo vim /usr/bin/gnome-terminal

# 第一行 由 python3 改为 python3.6
#!/usr/bin/python3.6
```

### 安装微信

参考链接：[deepin-wine-ubuntu](https://github.com/wszqkzqk/deepin-wine-ubuntu)

```bash
git clone https://github.com/wszqkzqk/deepin-wine-ubuntu.git

cd deepin-wine-ubuntu

./install.sh

chmod +x install_2.8.22.sh
./install_2.8.22.sh

# 下载微信安装包 http://packages.deepin.com/deepin/pool/non-free/d/deepin.com.wechat/
# 安装微信
sudo dpkg -i XXX.deb
```

## vscode

### 利用终端打开 vscode

在想要打开的目录下运行终端，输入如下命令：
```bash
code .
```

### 快捷键
| 快捷点组合           | 作用                               |
| -------------------- | ---------------------------------- |
| alt + 箭头上/箭头下  | 一行代码可以上下移动               |
| ctrl + shift + \     | 花括号跳转                         |
| ctrl + 箭头上/箭头下 | 光标停留在初始行不动，界面上下移动 |
| ctrl + Alt + Tab(ubuntu)     | 回退                               |

## 系统安装

### 安装虚拟机

安装 VMware 最新版本，否则虚拟机不好用。

### 安装双系统

安装大体步骤：

1. 制作u盘安装，Windows（官网可制作U盘或下载ISO）和Ubuntu（下载ISO后制作U盘，软件：[rufus](https://rufus.ie/downloads/)）；
2. 从U盘启动电脑；
3. 首先安装Windows系统，若遇到“无法在驱动器0的分区1上安装Windows”问题，百度可以解决；
4. 安装Ubuntu系统，在U盘启动电脑后选择第二个选项（install ubuntu，选择第一项可能将之前的Windows系统覆盖，这样安装完成后系统只要Ubuntu了）进行安装。


## Vim

### 基础配置

```bash
# 显示行号
set number

# 支持使用鼠标
set mouse=a

# 设置缩进
set autoindent
set tabstop=4
set shiftwidth=4
set expandtab
set softtabstop=4
```

参考链接：[阮一峰的网络日志:Vim 配置入门](https://www.ruanyifeng.com/blog/2018/09/vimrc.html)


## ROS

### 安装 rviz-visual-tools

```bash
sudo apt-get install ros-melodic-rviz-visual-tools
```

github 链接：[rviz-visual-tools](https://github.com/PickNikRobotics/rviz_visual_tools)

### 播放 rosbag 并在 RVIZ 中显示

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

### jsk_recognition_msgs/BoundingBoxArray.msg

编译出错：`fatal error: jsk_recognition_msgs/BoundingBoxArray.h: 没有那个文件或目录`

出错原因：重新安装 ros 之后，部分功能未安装

解决方法：

```bash
sudo apt-get install ros-melodic-jsk-recognition-msgs & sudo apt-get install ros-melodic-jsk-rviz-plugins
```

总结：没有消息类型可以使用 `sudo apt-get install ros-melodic-XXX` 进行安装，后面的安装语句不是所有的消息类型都有 rviz 插件。

