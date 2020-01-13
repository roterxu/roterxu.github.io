---
layout:     post                    # 使用的布局（不需要改）
title:      unbuntu安装docker-compose # 标题 
subtitle:   docker-composean安装 #副标题
date:       2019/12/13             # 时间
author:     XJ                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - docker-compose
---
## Hey

感觉官方提供的curl方法安装docker-compose 速度太慢   在这里提供一个pip安装docker-compose的方法
1:更新源
    
    sudo apt-install update

2:安装python pip
    
    sudo apt install python-pip

3：查看pip是否安装成功
    
    sudo pip --version

4:更新pip
    
    sudo pip install --upgrade pip

5:安装docker-conpose
    
    sudo pip install docker-compose

6:查看pip是否安装成功
    
    docker-comopse -v

7:更新docker-compose版本
    
    udo pip install --upgrade docker-comopse

到此  docker-compose安装成功  第一次写文章  又不足之处还请见谅
