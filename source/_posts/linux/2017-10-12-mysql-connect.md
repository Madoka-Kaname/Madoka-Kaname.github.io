---
title: 解决远程mysql数据库无法访问
date: 2017-10-12 16:29:22
categories: linux
tags:
- linux
- mysql
---

<!-- more -->

###### 解决方案

  1. 如果是云主机需要放通mysql端口, 一般为3306端口
  
  2. 如果有防火墙, 需要修改规则, 允许访问
    
     ```bash
     # 以centos7为例添加规则允许外界访问3306端口
     firewall-cmd —zone=public —add-port=3306/tcp —permanent
     # 重启防火墙
     systemctl restart firewalld.service
     ```
     
  3. 修改mysql权限
  
     - 修改访问规则并刷新规则
     
     ```mysql
     
     GRANT ALL PRIVILEGES ON *.* to 'root'@'%' IDENTIFIED BY 'ymP1TinRFxpm' WITH GRANT OPTION;
     FLUSH PRIVILEGES;
     ```
     
     - 重启mysql
     
     ```bash
     systemctl restart mysqld.service
     ```
     
     
    
    
