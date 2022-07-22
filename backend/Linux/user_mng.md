# 用户权限管理

## 创建用户
```shell
sudo su - root # 切换到root用户

# 新建用户
adduser test

# 给用户分配sudo权限
sudo usermod -a -G adm test
sudo usermod -a -G sudo test
```