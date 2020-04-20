---
layout:     post                    # 使用的布局（不需要改）
title:      mysqldump备份数据库              # 标题 
subtitle:   MySQL dump
date:       2019/04/20             # 时间
author:     XJ                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - mysql
---

## Hey

1:使用tmux 工具   tmux可以后台会话   比较方便 直接上命令
    
    mysqldump -hip -uroot -Pport -p --single-transaction --all-databases --master-data > all.sql
    

