---
title: 日常记录
date: 2024-07-15 14:19:45
tags:
---
# Windows端口被占用
7890端口被占用的问题，执行`netstat -ano | findstr ":7890"`查看当前端口占用情况

执行`netsh interface ipv4 show excludedportrange protocol=tcp`查看被排除的端口

# pip换源
```sh
pip install [包名] -i [pip源URL] 
```
```txt
阿里云: https://mirrors.aliyun.com/pypi/simple/
豆瓣: https://pypi.douban.com/simple/
清华大学: https://pypi.tuna.tsinghua.edu.cn/simple/
中国科学技术大学: https://pypi.mirrors.ustc.edu.cn/simple/
```
各版本Python下载链接 `https://www.python.org/ftp/python/`