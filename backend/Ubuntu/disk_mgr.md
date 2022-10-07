## 磁盘管理常用指令

### 查看当前磁盘信息

```shell
# 查看详细磁盘及分区信息
fdisk -l
# 查看已磁盘挂载信息
df -lh
# 列出所有磁盘及分区
lsblk
```

### 进行磁盘分区

这里将磁盘sdb划分为一个分区sdb1。如果要划分多个分区，在使用`n`指令时要注意提示输出对应参数值。

```shell
sudo fdisk /dev/sdb
# fdisk常用指令：
# m: 查看帮助
# n：新建分区
# d：删除分区
# wq：保存并退出
```

### 磁盘格式化

Linux支持多种文件系统，比如ext2, ext3, ext4等。在对磁盘进行分区后，需要将磁盘格式化为对应文件系统格式才能进行挂载和使用。

```shell
sudo mkfs.ext4 /dev/sdb1
```

### 磁盘挂载

将磁盘挂载在Linux的目录树上。如果挂载的目标下已经有其他的文件，则会使已有文件隐藏，它们将继续存在但无法被访问，在取消挂载后才会恢复。因此磁盘挂载一般需要创建一个新的目录后再进行。

```shell
sudo mount /dev/sdb1 /home/brandonye/data1
```

### 磁盘永久挂载

直接使用mount只能将磁盘临时挂载在系统上，重启后就会消失需要重新挂载。为了开机自动挂载，我们还需要做以下工作：

```shell
# 获取设备的UUID
sudo blkid /dev/sdb1
# 编辑文件fstab
sudo vim /etc/fstab

# 将以下指令加入到文件末尾
# <file system>    <mount point>    <type>   <options>    <dump>  <pass>
# UUID=48611660-38f5-4a8f-8ed5-89c08579ec09 /home/brandonye/data1   ext4     defaults     0       2
```

### 磁盘修复

当我们使用树莓派或Nano板时常常会用TF卡来存储系统等信息。不正当断电等方式有可能导致TF卡被写坏，此时我们需要对TF卡进行修复：

```shell
# 查看设备名
sudo lsblk
# 修复磁盘分区,一般是最大的那个
sudo fsck.ext4 /dev/sd{x}{n}
```