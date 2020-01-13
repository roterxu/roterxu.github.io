---
layout:     post                    # 使用的布局（不需要改）
title:      Docker部署rabbitmq               # 标题 
subtitle:   rabbitmq #副标题
date:       2019/12/11             # 时间
author:     XJ                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - docker
---

## Hey
>这是我的第一篇博客。

1:拉取rabbitmq镜像
    
    docker pull rabbitmq:management
    
2:运行镜像
    
    docker run -d --name rabbitmq --publish 5671:5671 \
     --publish 5672:5672 --publish 4369:4369 --publish 25672:25672 --publish 15671:15671 --publish 15672:15672 \
    rabbitmq:management

3:访问管理界面
    
    http://[宿主机IP]:15672
   
4：修改管理员密码
    
    docker exec -it myrabbit1 bash     #进入容器
    rabbitmqctl  list_users      #查看用户列表
    rabbitmqctl  change_password  Username  'Newpassword'     #修改用户密码
    
