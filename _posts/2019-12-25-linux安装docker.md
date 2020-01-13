---
layout:     post                    # 使用的布局（不需要改）
title:      CentOS Docker 安装 # 标题 
subtitle:   CentOS Docker 安装 #副标题
date:       2019/12/25            # 时间
author:     XJ                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - CentOS Docker 安装
---

1:首先卸载docker的旧版本
    
    sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine

2:安装所需的软件包

    sudo yum install -y yum-utils \
        device-mapper-persistent-data \
        lvm2
    
3:设置稳定仓库
    
    sudo yum-config-manager \
        --add-repo \
        https://download.docker.com/linux/centos/docker-ce.repo
    
阿里云仓库
        
    sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

4:更新yum包索引
    
    sudo yum makecache fast
    
5:安装Docker
    
    sudo yum install docker-ce
    
6:安装指定版本docker
    
    sudo yum install docker-ce-<VERSION>
    
7:启动docker
    
    sudo systemctl start docker
    
8:验证docker是否安装成功

    sudo docker run hello-world
    
9:Dockerfile
    
    FROM java:8
    VOLUME /tmp
    ADD md5-query-web-1.0-SNAPSHOT.jar app.jar
    RUN bash -c 'touch /app.jar'
    EXPOSE 9000
    ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","app.jar"]
    
10:jar包放在Dockerfile相同目录下  通过docker build创建镜像

    