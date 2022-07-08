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
