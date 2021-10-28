# git 安全与验证

## 设置密码缓存

为了避免每次修改仓库都要重新输入账户名和密码，我们可以设置密码缓存

```shell
git config --global credential.helper cache         # 缓存一定时间后自动删除
git config --global credential.helper store         # 永久存储

# 如果需要删除密码重新输入, 则重新设置一次即可
git config --global --unset credential.helper
git config --global credential.helper store
```