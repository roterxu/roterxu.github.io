---
layout:     post                    # 使用的布局（不需要改）
title:      使用docker安装mysql 安装 # 标题 
subtitle:   docker安装mysql #副标题
date:       2019/12/26            # 时间
author:     XJ                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - docker 
---

1:首先拉取mysql镜像 docker pull mysql 默认是最新版本  也可以指定版本  docker pull mysql:5.7.19
    
    docker pull mysql
    docker pull mysql:5.7.19
       
2:查看镜像：docker images  可查看已拉取的镜像
    
    docker images
    
3：安装mysql
    
    docker run --name mysql -d \               #  此行的mysql为容器名称
    -v /data/docker/mysql/data:/var/lib/mysql \       #硬盘挂载
    -v /data/docker/mysql/logs:/logs \
    -v /data/docker/mysql/conf:/etc/mysql/conf.d \
    -e MYSQL_ROOT_PASSWORD=123456 \       #初始密码
    -e TZ=Asia/Shanghai \            #设置时区
    -p '3310:3306' \                #端口映射    连接mysql是使用3310d端口
    mysql:5.7.19 \                  #镜像版本
    
4: 查看mysql安装是否成功  docker ps    可查看已启动的镜像
    
    docker ps
    
5：进入mysql容器    
    
    docker exec -it mysql bash       

6：开启mysql远程连接权限  进入mysql执行:
    
    ALTER  USER  'root'  IDENTIFIED  WITH  mysql_native_password  BY  'newpassword'; 
    
