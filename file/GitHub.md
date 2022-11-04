# GitHub

## 更换电脑后，git clone 出错

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



## 生成 tokens

在本地远程推送时，有时候需要输入 username 和 password，password 不是登录 github 时的密码，而是 tokens，在哪生成 tokens ？

Settings/Developer settings/Personal access tokens



## 切换分支

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



## 新建分支并上传代码

```bash
# 查看所在分支
git branch

# 切换至 master 分支
git checkout master

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

# 在 UI 界面提交合并请求
```

注：提交的时候，先去 master 分支 git pull 一下，再去新建分支更新内容，否则在别的分支 git pull，然后再将新建的分支合并到 master 可能会出现 rebase 情况，这是由冲突导致的，别人在 master 提交了代码，你没有更新却还想往 master 上面 push 。



## 删除分支

```bash
git branch -d 分支名
git branch -D 分支名		# 强制删除
```



## git commit 后撤销

```bash
# 撤销 commit，不撤销 add
git reset --soft HEAD^

# 同时撤销 commit 和 add
git reset --hard HEAD^
```



## 回退到之前版本

提交当前修改后，想撤销此次修改，并回退到之前版本，注：已 commit、push。

```bash
git log	# 将显示提交的历史
#commit 809f4158ca76baeddbb8d8cb8c6a87e990a6bf7e (HEAD -> ev/mm, origin/ev/mm)  （commit id 以及分支名）
#Author: XXX （作者）
#Date:   Fri Nov 4 16:16:59 2022 +0800 （时间）

#    XXX（commit 注释信息）

git reset --hard id # 想要回退版本的 id

git push origin HEAD --force
```

