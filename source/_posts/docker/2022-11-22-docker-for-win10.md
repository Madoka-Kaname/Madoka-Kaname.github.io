---
title: win10系统安装使用docker
date: 2022-11-22 21:29:26
categories: docker
tags:
- docker
- php
- linux
---

### 准备
  
  - Docker Desktop 
     
     ###### 官网地址 (https://www.docker.com/)
  
### 电脑bios开启支持vt虚拟化

### win10系统开启wsl(建议)或者hyper-v

   - 搜索栏搜启动或关闭windows功能，设置好后重启电脑
   
### 启动docker, 配置阿里云镜像加速, 然后重启docker

   ```json
        {
          "registry-mirrors": ["https://qundbw00.mirror.aliyuncs.com"]
        }
   ```

### 拉取`centos:8`官方镜像

### 创建`centos8`容器

  - `powershell`管理员命令行执行
  
    ```bash
    docker run -itd --volume=C:\Users\wanghuan\Code:/data --name centos8 --privileged centos:8 /usr/sbin/init
    ```
    
  - 如果docker卡住或出现权限问题, `powershell`管理员命令行执行, 然后重启docker
  
    ```bash
    cd "C:\Program Files\Docker\Docker"
    ./DockerCli.exe -SwitchDaemon
    ```
    
  - 进入容器后yum出现`Failed to download metadata for repo ‘AppStream’: Cannot prepare internal mirrorlist: No URLs in mirrorlist”`错误
  
    ```bash
    # 进入yum的repos目录
    cd /etc/yum.repos.d/
    
    # 修改所有的CentOS文件内容
    sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
    sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
    
    # 更新yum源为阿里镜像
    yum install wget -y
    wget -O /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-vault-8.5.2111.repo
    yum clean all
    yum makecache
    ```  

### 安装`lnmp`和`node js`环境

  ```bash
    # 安装oneinstack
    yum -y install epel-release
    yum -y install wget screen
    wget http://mirrors.linuxeye.com/oneinstack-full.tar.gz
    tar xzf oneinstack-full.tar.gz
    cd oneinstack
    screen -S oneinstack
    ./install.sh

    # 重新加载环境变量
    source /etc/profile
  ```

### 安装git

  ```bash
    yum install git
    ssh-keygen -t rsa -C 
  ```
