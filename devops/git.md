# Git 工具

## Git 代理设置

在国内访问github速度很慢，可以在本地开启代理，并配置git使用代理服务：

```shell
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080'
```

## Git 设置密码缓存

为了避免每次修改仓库都要重新输入账户名和密码，我们可以设置密码缓存

```shell
git config --global credential.helper cache         # 缓存一定时间后自动删除
git config --global credential.helper store         # 永久存储

# 如果需要删除密码重新输入, 则重新设置一次即可
git config --global --unset credential.helper
git config --global credential.helper store
```



## 使用Git更新仓库流程

1. 如果仓库是private的，使用git拉取仓库时需要加上github账号的用户名和密码：

```shell
git clone https://github-username:github-password@github.com/Yunxuan-Develop/repository-name.git
```

&emsp; &ensp;&nbsp;不是private的话：

```shell
git clone https://github.com/Yunxuan-Develop/repository-name.git
```

2. 将新代码复制进拉取下来的文件夹中：

```shell
cp -rf new-code-path/* ./repository/
```

&emsp; &ensp;&nbsp;参数`-r`：复制源文件夹中文件夹，参数`-f`：覆盖已经存在的目标文件而不给出提示

&emsp; &ensp;&nbsp;注意，上述命令无法复制隐藏文件（例如文件名以'.'开头的文件），隐藏文件需要单独进行处理

3. 将所有文件添加进仓库中：

```shell
git add .
```

&emsp; &ensp;&nbsp;单独添加某一文件：

```shell
git add file-name
```

4. 查看文件状态，红色为未添加，绿色为已添加：

```shell
git status
```

5. 提交修改：

```shell
git commit -m 'messsage'
```

&emsp; &ensp;如果是第一次提交，需要先进行以下git配置（github账号设置的邮箱和用户名）：

```shell
git config --local user.email "you@example.com"
git config --local user.name "Your Name"
```

&emsp; &ensp;&nbsp;因为服务器上是多人进行操作，需要注意配置的范围，合理选择`--global`还是`--local`，[详情点击我](https://blog.csdn.net/qq_29827369/article/details/106294460)

6. 查看提交情况：

```shell
git log
```

7. 最后，将新仓库提交到github上：

```shell
git push
```

## Git的撤销回退操作

如果发现`git commit -m`的信息写错了，或者`git add`错文件了，可以按照下面的流程重新修改并提交

1. 回退到上一版本：

```shell
git reset [--soft][--mixed][--hard] HEAD^
```

&emsp; &ensp; `--soft`不会改变`git add`以及当前工作目录的内容，只是将commit状态回退

&emsp; &ensp;&nbsp;`--mixed`撤销此次`git add`，同时回退commit状态，但不会改变当前工作目录的内容

&emsp; &ensp; `--hard`撤销此次`git add`，同时回退commit状态，当前工作目录的内容也会回到上一个版本

&emsp; &ensp;&nbsp;[详情点击我1](https://www.jianshu.com/p/c6927e80a01d)

&emsp; &ensp;&nbsp;[详情点击我2](https://www.runoob.com/git/git-reset.html)

2. 重新添加修改后，进行提交：

```shell
git commmit --amend
git push -f
```

如果还未`git add`或者`git commit`，想要撤销修改某个文件，可以使用下面的命令：
```shell
git checkout -- file-name
```