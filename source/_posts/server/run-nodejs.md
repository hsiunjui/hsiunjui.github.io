---
title: pm2启动nodejs项目
date: 2025-03-02 20:11:02
tags: 服务器
categories: 运维
---
>centos 运行nodejs项目.

<!--more-->

# 安装nodejs
```
sudo yum update -y
curl -fsSL https://rpm.nodesource.com/setup_18.x | sudo bash -
sudo yum install -y nodejs

node -v
npm -v
```

# 传送文件
```bash
scp ~/Downloads/dist.zip root@192.168.1.100:/root/ #上传
unzip dist.zip # sudo yum install -y unzip

scp root@192.168.1.100:/root/dist.zip ~/Downloads/dist.zip #下载
```

# 安装pm2
```bash
sudo npm install -g pm2
```

## pm2 相关命令
```bash
cd project
pm2 start app.js

pm2 list	#查看所有运行中的进程
pm2 status	#查看进程状态
pm2 restart app.js	#重启应用
pm2 stop app.js	#停止应用
pm2 delete app.js	#删除应用
pm2 logs	#查看日志

pm2 startup #服务器重启后，PM2 自动启动 (sudo systemctl enable pm2-root)
pm2 save #保存当前运行的应用,PM2 会在系统启动时自动恢复所有进程
```

# 开放端口
```bash
sudo systemctl status firewalld #查看

sudo systemctl start firewalld # 开启
sudo systemctl enable firewalld  # 开机自启

sudo firewall-cmd --zone=public --add-port=3000/tcp --permanent # 开放3000端口
sudo firewall-cmd --reload #重载防火墙

sudo firewall-cmd --list-ports # 查看开放的端口


```