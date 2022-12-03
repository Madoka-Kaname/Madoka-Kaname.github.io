---
title: Node js环境安装和配置
date: 2018-11-21 14:40:33
categories: node js
tags:
- node js
---

> 现在的前端开发已经离不开nodejs，其中的npm（或yarn）包管理工具更是带来很好的开发体验是。本文将简单介绍nodejs的安装及环境变量的配置，方便在更换电脑后重新配置node的查阅。

##### nodejs下载及安装

  - 下载node.js安装包
  
    ```bash
    wget https://nodejs.org/dist/v16.18.0/node-v16.18.0-linux-x64.tar.xz
    ```
    
  - 解压缩并安装
  
    ```bash
    tar -xvf node-v16.18.0-linux-x64.tar.xz
    mv node-v16.18.0-linux-x64/* /usr/local/node
    rm -rf ./node-v16.18.0-linux-x64
    ```
    
  - 配置node 环境变量
  
    ```bash
    vim /etc/profile
    ```
    
  - 追加环境变量
  
    ```bash
    export NODE_HOME=/opt/node
    export PATH=$PATH:$NODE_HOME/bin
    export NODE_PATH=$PATH:$NODE_HOME/lib/node_modules
    ```
  
  - 刷新环境变量, 使配置生效
  
    ```bash
    source /etc/profile
    ```
    
  - 查看是否安装成功
  
    ```bash
    node -v
    npm -v
    ```
    
  - 更换淘宝node镜像
  
    ```bash
    npm config set registry https://registry.npm.taobao.org 
    npm config get registry 
    ```

##### 安装yarn等组件

   - 安装yarn
   
     ```bash
     npm install -g yarn
     yarn --version
     ```
     
   - 安装vue-cli
   
     ```bash
     npm install -g @vue/cli
     ```
     
   - 安装`cnpm`
   
     ```bash
     cnpm install
     npm install -g cnpm --registry=https://registry.npm.taobao.org
     ```
    

  

  








    