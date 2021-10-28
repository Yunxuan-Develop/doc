# git 子模块

## 添加子模块

当我们希望在我们的仓库中引用其他人的仓库作为子模块时，我们可以如下添加：

```shell
# url代表目标仓库路径 path代表你想要把子模块存储在哪里，一般可以不填
$ git submodule add <url> <path>
```

## 下载子模块

在我们克隆一个包含子模块的仓库后，会发现子模块的代码没有被下载，此时我们应该输入：

```shell
$ git submodule update --init --recursive
```

## 子模块更新

子模块维护者提交了更新后，我们可以手动将子模块更新到最新版本

```shell
$ cd PATH_TO_MODULE
$ git pull
```


