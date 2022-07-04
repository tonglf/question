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
