---
title: 清理VMware磁盘空间
date: 2024-07-14 17:14:12
tags:
indexing: true
---
填充磁盘空间（做）
接下来，我们可以使用一个二进制0的文件来填充所有磁盘空间，并通过删除该文件来释放空间。按照以下步骤进行操作：

执行命令 `sudo apt-get clean` 清除残留的安装包（此步骤可选）。
执行命令 `sudo dd if=/dev/zero of=/0bits bs=20M`，将碎片空间填充为0。在执行过程中，可能会提示磁盘空间不足，但可以忽略该提示。

执行命令 `sudo rm -rf /0bits`，删除第二步中填充的文件。使用命令 df -h 可以发现可用的虚拟空间增加了很多，但实际的磁盘空间并没有减少。
收缩根目录->平台特定清理命令
最关键的一步是在虚拟机中收缩根目录。
`.\vmware-vdiskmanager.exe -k D:\Vmware\Ubuntu2204\Ubuntu2204.vmdk`