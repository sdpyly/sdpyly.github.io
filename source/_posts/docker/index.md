---
title: Docker记录
date: 2024-07-14 17:08:29
tags: docker
---
# 安装注意事项
可按照官网安装步骤，注意以下事项

将gpg文件放在/etc/apt/keyrings/docker.asc 重命名 sudo chmod a+r /etc/apt/keyrings/docker.asc

执行
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://mirrors.aliyun.com/docker-ce/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

确保/etc/apt/sources.list.d/docker.list的内容为
deb [arch=amd64 signed-by=/etc/apt/keyrings/docker.asc] https://mirrors.aliyun.com/docker-ce/linux/ubuntu   jammy stable

将models放在/home/ubuntu/Code/SecGPT目录下，做端口映射和目录挂载
docker run -p 8080:7860 -d -v D:\Projects\PythonProjects\SecGPT\models:/secgpt-mini/models d1655c1ed1f2

# 命令记录
进入容器命令行
`docker run -p 8080:7860 -it -v /home/ubuntu/Code/SecGPT/models:/secgpt-mini/models 1c5554c6582a /bin/bash`

遇到该问题是transformer版本的问题，pip install  transformers==4.40  -i https://mirrors.aliyun.com/pypi/simple/
ValueError: Tokenizer class Qwen2Tokenizer does not exist or is not currently imported.
https://blog.csdn.net/zengNLP/article/details/138320888

docker构建 `docker build -t secgpt_total:latest .`

docker保存 `docker save -o secgpt_total.tar secgpt_total:latest`

docker清缓存 `docker system prune`