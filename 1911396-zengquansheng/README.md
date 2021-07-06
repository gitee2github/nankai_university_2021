# openEuler开源创新实践课

1911396-曾泉胜

## 实验内容

本次实验在虚拟机上安装了openEuler操作系统，并以之为宿主机，在其上构建了LFS系统

实验主要流程如下：

- 配置虚拟机
- 安装openEuler操作系统
- 为LFS系统做准备（新建磁盘分区，下载补丁、压缩包等）
- 创建lfs用户，编译临时工具
- 使用上一步得到的编译器在chrooted下编译
- 系统配置、编译安装内核
- 设置grub使系统可引导

## 遇到的问题

我先是VMware上安装虚拟机作为宿主机，基本配置如下图

![3](failure\3.png)

其中SCSI的硬盘上是宿主机的操作系统，SATA的硬盘上是LFS的操作系统，接着按照指导书+脚本+文档，复制粘贴指令就行。。。

在`make menuconfig`时，对于指导书中

> 比如说，如果您安装了SCSI的硬盘，则需要选择以下配置

这部分的内容，我并没有理会（因为我认为我LFS系统挂载在SATA磁盘上），只是按照接下来的要求进行了配置。

但不幸的是，最终在启动系统是仍然因为不清楚的原因失败了，如下图所示：

![0](failure\0.png)

![1](failure\1.png)

![2](failure\2.png)

关于错误VFS:Unable to mount root fs on unknown-block(0.0)，参考

[CSDN-whatday](https://blog.csdn.net/whatday/article/details/104760046)说是`/boot`盘空间不够；参考[跳墙网-神秘网友](https://www.tqwba.com/x_d/jishu/195629.html)说是根目录文件系统出现了问题；参考[Stack-exchange](https://unix.stackexchange.com/questions/414655/not-syncing-vfs-unable-to-mount-root-fs-on-unknown-block0-0)可能是内核不支持设备上的文件系统，或者传递给内核的根设备名称是错误的。

本人能力有限，且时间也比较短，也许尝试在`make menuconfig`时开启了SCSI的相关配置可能有帮助？

但是我选择了更粗暴简单的办法，按照老师说的，使用VituralBox重新开始吧。。。

最后成功的截图如下：

![1911396-zengqs-1](success\1911396-zengqs-1.png)

![1911396-zengqs-1](success\1911396-zengqs-1.png)

