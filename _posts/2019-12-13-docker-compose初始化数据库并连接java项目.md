---
layout:     post                    # 使用的布局（不需要改）
title:      docker-compose启动！java动态加载docker中的数据库 # 标题 
subtitle:   docker-compose         #副标题
date:       2019/12/11             # 时间
author:     XJ                     # 作者
header-img: img/post-bg-2015.jpg   #这篇文章标题背景图片
catalog: true                      # 是否归档
tags:                              #标签
    - docker-compose
---
关于docker-compose安装上一篇已经讲过了  这里就不做叙述！  
首先文件结构

    deploy: 
            |docker-compose.yml  
            |md5  
            |mysql1  
            |mysql2  
        
docker-compose.yml为配置文件   书写时注意格式   

    version: '3'
    services:
     mysql1:
      image: mysql:5.6
      ports:
       - "3307:3306"
      container_name: mysql1
      environment:
       MYSQL_DATABASE: mysql1
       MYSQL_USER: admin
       MYSQL_PASSWORD: admin
       MYSQL_ROOT_PASSWORD: admin
       MYSQL_ROOT_HOST: '%'
      volumes:
       - ./mysql1/data:/var/lib/mysql          #硬盘挂载    
       - ./mysql1/init:/docker-entrypoint-initdb.d/
       - ./mysql1/conf:/etc/mysql
     mysql2:
      image: mysql:5.6
      ports:
       - "3308:3306"
      container_name: mysql2
      environment:
       MYSQL_DATABASE: mysql2
       MYSQL_USER: admin
       MYSQL_PASSWORD: admin
       MYSQL_ROOT_PASSWORD: admin
       MYSQL_ROOT_HOST: '%'
      volumes:
       - ./mysql2/data:/var/lib/mysql
       - ./mysql2/init:/docker-entrypoint-initdb.d/
       - ./mysql2/conf:/etc/mysql
     query:
      build: ./md5/
      ports:    # 指定端口映射  
        - "9000:8080"
      depends_on:    #防止java项目启动时数据库初始化为完成，这里depends_on  是query依赖前两个服务启动   
        - mysql1
        - mysql2


MD5目录结构(我的项目是md5解密所以叫MD5)
    
    md5:
        Dockerfile    
        ***.jar        
    
Dockerfile
    
    FROM java:8
    VOLUME /tmp
    ADD ***.jar app.jar    
    RUN bash -c 'touch /app.jar'
    EXPOSE 9000
    ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","app.jar"]
    
***.jar文件是你的java包

mysql1目录

    mysql1:
           -conf
           -init:
                -init.sql     初始化文件放在这  如果启动docker不需要初始化数据库则可以不放
           -logs
mysql2目录个mysql1目录相同  这里就不写了

java项目配置文件  
application-docker.yml
这里端口号一定要写映射前的端口号！  
我自己当初是在这踩的坑

      mysql1: #    这里端口号一定要写映射前的端口号
        url: "jdbc:mysql://mysql1(docker-compose.yml里面的服务名):3306/phone_md5?allowMultiQueries=true&useUnicode=true&useSSL=false&characterEncoding=UTF-8&allowPublicKeyRetrieval=true"
        username: "root"
        password: "admin"
        driverClassName: com.mysql.jdbc.Driver
      mysql2: # 
        url: "jdbc:mysql://mysql2(docker-compose.yml里面的服务名):3306/phone_md5?allowMultiQueries=true&useUnicode=true&useSSL=false&characterEncoding=UTF-8"
        username: "root"
        password: "admin"
        driverClassName: com.mysql.jdbc.Driver

在deploy目录下执行

    dcoker-compose up -d

查看容器是否创建成功  docker ps
    
    docker ps

进入容器查看数据库是否初始化
    
    docker exec -it mysql1 bash    

查看java项目是否启动成功   一般情况下 数据库失败的话  项目连接数据库就会报错
    
    docker logs -f CONTAINER ID    (项目的容器id)
    
  
