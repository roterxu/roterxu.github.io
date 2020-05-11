---
layout:     post                    # 使用的布局（不需要改）
title:      Java8Stream              # 标题 
subtitle:   Java8
date:       2020/04/21             # 时间
author:     XJ                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - stream
---

## Java8中Stream处理集合非常方便  记录一下方便自己使用

1:list转Map
    
    List<User> userList=new ArrayList();
    userList.add(use);//自己创建对象插入userList即可
    Map<Integer, User> collect = UserList.stream().collect(Collectors.toMap(User::getId, u -> u));

2:map转list
    
    Map<Integer, User> userMap=new HashMap();
    List<User> userList = new ArrayList<>(userMap.values());
    
3:list分组成map  
    
    List<User> userList=new ArrayList();
    Map<String, List<User>> userMap = userList.stream().filter(u -> StringUtils.isNotBlank(u.getUserName)).collect(Collectors.groupingBy(u -> u.getPhone()));
    filter里面时过滤条件 不符条件的背剔除