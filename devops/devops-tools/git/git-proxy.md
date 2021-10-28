# git 代理设置

## git 代理设置

在国内访问github速度很慢，可以在本地开启代理，并配置git使用代理服务：

```shell
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080'
```