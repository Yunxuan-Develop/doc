# git 全局配置

## 设置密码缓存

为了避免每次修改仓库都要重新输入账户名和密码，我们可以设置密码缓存

```shell
git config --global credential.helper cache         # 缓存一定时间后自动删除
git config --global credential.helper store         # 永久存储

# 如果需要删除密码重新输入, 则重新设置一次即可
git config --global --unset credential.helper
git config --global credential.helper store
```

## git 代理设置

在国内访问github速度很慢，可以在本地开启代理，并配置git使用代理服务：

```shell
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080'
```