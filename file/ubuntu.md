# ubuntu

## 终端快捷键

- 打开新终端：Ctrl + Alt + t
- 新建标签页：Ctrl + Shift + t
- 切换标签页：Alt + 1/2/3(标签页顺序)
- 关闭标签页：Ctrl + d

更多快捷键内容，在终端点击按钮查看：`编辑`->`首选项`->`快捷键`

## 终端按 ctrl+s 就卡住

如果在终端按了组合键 **ctrl+s**，会发现终端按什么键都没反应，感觉终端卡住了，这是怎么回事呢？

其实，终端处于假死的状态，这个是 linux 系统命令行模式下的锁屏快捷键，只是输入的命令没有在输出终端（显示器）显示出来而已。
要退出此种锁屏界面，需按 **ctrl+q**，此时会发现先前在锁屏时输入的字符都显示出来了，并且可正常使用了。

## 查看 IP 地址

```bash
ifconfig -a
```

注：

1. `ifconfig` 命令需要安装，安装命令如下：

   ```bash
   sudo apt install net-tools -y
   ```

2. 由 `ifconfig -a` 显示的内容，第三部分，`inet` 对应的地址为本机对应的 ipv4 地址。



## 不同软件版本切换

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



## gcc/g++ 不同版本的切换

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



## ubuntu 18.04 python 升级之后，终端打不开

ubuntu 18.04 python 由 3.6 升级到 3.7 之后，终端不能直接打开，需要右键选择在终端打开才行

解决方法：修改文件内容

```bash
sudo vim /usr/bin/gnome-terminal

# 第一行 由 python3 改为 python3.6
#!/usr/bin/python3.6
```



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



## dpkg

### 安装

```bash
sudo dpkg -i XXX.deb
```

### 卸载

```bash
# 卸载
sudo dpkg -r XXX

# 卸载并删除配置文件    
sudo dpkg --purge XXX    
```

### 查看

```bash
# 显示所有安装的软件
dpkg -l 

# 查找安装软件的名称(不知道软件的名称，XXX写个大概，然后查询)
dpkg -l | grep XXX
```

更多命令，参考：`dpkg --help`。



## conda

```bash
# 创建虚拟环境（后面是Python版本）
conda create --name my_first_env python=3.6

# 列出存在的虚拟环境
conda env list

# 进入某个虚拟环境
conda activate virtual_env

# 如果进不去，先输入以下命令再进入
source activate

# 显示环境内安装的软件
conda list

# 安装与卸载
pip install
pip uninstall
conda install
conda uninstall 

# 退出虚拟环境
conda deactivate

# other
# 默认不进入 base
conda config --set auto_activate_base false
```



## 安装视频播放软件 mpv

```bash
sudo apt-get update

sudo apt-get install mpv
```



## 安装微信

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



## 微信输入框中文显示方框

系统语言非中文时，中文全显示成方块，需要在 `/opt/deepinwine/tools/run.sh` 中将 WINE_CMD 那一行修改为

```bash
WINE_CMD="LC_ALL=zh_CN.UTF-8 deepin-wine"
```

参考链接：[ubuntu18.04下 中文字体显示为方块 方框 #136](https://github.com/wszqkzqk/deepin-wine-ubuntu/issues/136)

如果之后又出现上述情况，重启微信即可。



## 安装搜狗输入法，不能输入中文

Ubuntu 18.04 安装搜狗输入法后，只能输入英文，不能输入中文，可能是缺少安装依赖，解决方法是在完成安装搜狗输入法后，安装如下依赖：

```bash
sudo apt install libqt5qml5 libqt5quick5 libqt5quickwidgets5 qml-module-qtquick2
 
sudo apt install libgsettings-qt1
```

参考博客：[ubuntu 20.04 安装好搜狗输入法无法输入中文，只能输入英文的问题，因为没有安装依赖](https://blog.csdn.net/ccsodefhy/article/details/123122200)

