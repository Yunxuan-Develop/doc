# 开发流程及规范

## 使用Git branch进行开发

在向git提交代码时，严格禁止直接将代码提交到master分支上（尤其是使用 git push -f 的时候需要十分小心）。master分支上的代码必须是经过测试后稳定可用的，以确保每一个commit都是一个稳定可用的版本，以便于出现异常时迅速进行代码回滚。

因此在配置开发环境时，我们需要按照以下流程进行：

```bash
# 1. 从git上拉取代码
git clone https://github.com/Yunxuan-Develop/repo_name.git

# 2. 进入代码路径
cd repo_name

# 3. 新建开发分支
# branch_name一般命名为 brandonye/xxx （xxx 为当前分支开发内容名字）
git checkout -b branch_name

# 执行完后你会自动切换到要开发的分支上（master本身其实也是一个普通的分支）
# 正式开发前请到 https://github.com/Yunxuan-Develop/table 中创建issue并记录问题描述和解决方法。

# 进行一系列开发工作...

# 4. 提交修改：
# 查看当前修改
git status

# add当前issue相关的修改文件
git add xxx

# commit修改
# message 一般格式为 "$purpose: $msg.($issueID)"
# 	$purpose: feat(增改功能), bug(修理bug)
#	$msg: 这个commit的描述
#   $issueID: 这个commit对应的issue id, 例如Yunxuan-Develop/table#1
git commit -m "message"

# 推送git branch
git push origin brandonye/xxx:brandonye/xxx

# 在测试机上拉取对应分支的代码进行部署测试
# 测试完成后在git页面上发起Pull Request
# PR 的 信息填写当前pr关联的issueID，例如Yunxuan-Develop/table#1。（关联成功是蓝色可跳转字样）
# 最后通知 reviewer 评审代码，评审approve后可以合入master
```

其他一些相关的Git branch和Git操作：

```bash
# 删除分支
git branch -d localbranch
git push origin --delete remotebranch

# 查看当前分支
git branch -l

# 更新本地代码（最好保证本地master和远端master代码完全一致的）
git checkout master
git pull
git checkout yourbranch
git merge master

# 撤回上一次commit
git reset --soft HEAD^              # 保留commit的代码
git reset --hard HEAD^              # 不保留代码
# 回退到某一次commit
git reset --soft(hard) commid_id    # 返回某一次的commit
```

