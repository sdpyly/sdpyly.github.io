---
title: linux系统初始化
date: 2024-07-14 17:11:36
tags: initialize
---
包含Ubuntu、Centos等虚拟机，也包含raspberry等设备
# 无显示器的树莓派配置
在Linux命令行下，执行`echo 'raspberry' | openssl passwd -6 -stdin`获得密钥

创建userconf.txt文件，内容形如
```txt
pi:$6$/4.VdYgDm7RJ0qM1$FwXCeQgDKkqrOU3RIRuDSKpauAbBvP11msq9X58c8Que2l1Dwq3vdJMgiZlQSbEXGaY5esVHGBNbCxKLVNqZW1
```

创建一个名为ssh的空文件，开启ssh服务

# 安装常见软件
vim git gcc g++ net-tools tmux
# 配置代理
```sh
export http_proxy=http://192.168.10.199:7890
export https_proxy=http://192.168.10.199:7890
```
# 安装oh-my-posh
需先配置代理
```sh
mkdir bin
curl -s https://ohmyposh.dev/install.sh | bash -s -- -d ~/bin
export PATH=$PATH:/home/pi/bin # 注意修改用户名

oh-my-posh font install
# 不存在该文件时新建
sudo mkdir /usr/share/fonts/ttf
# 下载好的文件放入ttf文件中
sudo cp *.ttf /usr/share/fonts/ttf
# 给予权限
cd /usr/share/fonts/ttf
sudo chmod 744 *
# 重新生成索引
sudo fc-cache -f -v
```
在.bashrc或.zshrc中写入，注意修改用户名
```sh
export PATH=$PATH:/home/pi/bin
eval "$(oh-my-posh init bash --config /home/pi/.cache/oh-my-posh/themes/robbyrussell.omp.json)"
```
# 配置ssh公钥登录
创建公私钥对，形如`ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f ~/.ssh/your_custom_name`

若无~/.ssh目录，可执行`ssh ubuntu@127.0.0.1`输入yes创建一个

在.ssh目录下创建`authorized_keys`文件，写入公钥

修改文件权限为600

客户端配置~/.ssh/config，形如
```txt
Host localubuntu
	HostName 192.168.73.133
	User ubuntu
	Port 22
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/local
```