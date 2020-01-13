---
layout:     post                    # 使用的布局（不需要改）
title:      使用docker安装redis 安装 # 标题 
subtitle:   docker安装redis #副标题
date:       2019/12/26            # 时间
author:     XJ                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - docker 
---

1:拉取redis镜像   这是拉取最新版镜像，也可自定义版本
    
    docker pull redis:latest

2:查看镜像 docker images
    
    docker images

3:运行容器   "password" 放你的redis密码
    
    docker run -d --name myredis -p 6379:6379 redis --requirepass "password"

4:通过docker ps查看容器
   
    docker ps

5进入容器
    
    ocker exec -it myredis /bin/bash