# 分支管理

## 创建本地分支

在本地创建分支

```shell
$ git checkout -b branch_name
```

## 推送本地分支到远程

将本地分支代码推送到远端

```shell
$ git push origin local_branch_name:remote_branch_name
```

## 删除分支

### 删除本地分支

```shell
$ git branch -d LocalBranchName
```

### 删除远程分支

```shell
$ git push origin --delete RemoteBranchName
```


