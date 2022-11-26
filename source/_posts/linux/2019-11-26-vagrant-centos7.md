---
title: 使用vagrant安装centos7虚拟机
date: 2019-11-26 20:04:36
categories: linux
tags:
- vagrant
- linux
---

##### 准备
  
  - vagrant2.2.19_x86_64.msi([官方下载地址](https://releases.hashicorp.com/vagrant/2.2.19/vagrant_2.2.19_x86_64.msi))
     
  - VirtualBox-6.1.32-149290-Win.exe([官方下载地址](https://download.virtualbox.org/virtualbox/6.1.32/VirtualBox-6.1.32-149290-Win.exe))
  
  - CentOS-7-x86_64-Vagrant-2004_01.VirtualBox.box([官方下载地址](http://cloud.centos.org/centos/7/vagrant/x86_64/images/CentOS-7-x86_64-Vagrant-2004_01.VirtualBox.box))
  
   
##### 安装虚拟机

   - 添加box
       ```bash
       # 进入box存放目录
       cd ~/vagrant/box
       # 添加box到vagrant
       vagrant box add CentOS-7-x86_64-Vagrant-2004_01.VirtualBox.box
       # 查看box列表
       vagrant box list
       ```
   - 安装vagrant plugin
       ```bash
       # 查看vagrant-vbguest是否安装, 未安装则无法挂载目录进行数据持久化
       vagrant plugin list
       # 安装0.24版本 
       vagrant plugin install vagrant-vbguest --plugin-version 0.24
       ```
   - 初始化
       ```bash
       cd ~/vagrant
       vagrant init
       ```
   - 配置`Vagrantfile`文件
       ```shell script
       # -*- mode: ruby -*-
       # vi: set ft=ruby :
       
       # All Vagrant configuration is done below. The "2" in Vagrant.configure
       # configures the configuration version (we support older styles for
       # backwards compatibility). Please don't change it unless you know what
       # you're doing.
       Vagrant.configure("2") do |config|
         # The most common configuration options are documented and commented below.
         # For a complete reference, please see the online documentation at
         # https://docs.vagrantup.com.
       
         # Every Vagrant development environment requires a box. You can search for
         # boxes at https://vagrantcloud.com/search.
         config.vm.box = "centos7"
         config.vm.hostname = "centos"
       
         # Disable automatic box update checking. If you disable this, then
         # boxes will only be checked for updates when the user runs
         # `vagrant box outdated`. This is not recommended.
         # config.vm.box_check_update = false
       
         # Create a forwarded port mapping which allows access to a specific port
         # within the machine from a port on the host machine. In the example below,
         # accessing "localhost:8080" will access port 80 on the guest machine.
         # NOTE: This will enable public access to the opened port
         # config.vm.network "forwarded_port", guest: 80, host: 8080
       
         # Create a forwarded port mapping which allows access to a specific port
         # within the machine from a port on the host machine and only allow access
         # via 127.0.0.1 to disable public access
         # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
       
         # Create a private network, which allows host-only access to the machine
         # using a specific IP.
         config.vm.network "private_network", ip: "192.168.56.10"
       
         # Create a public network, which generally matched to bridged network.
         # Bridged networks make the machine appear as another physical device on
         # your network.
         # config.vm.network "public_network"
       
         # Share an additional folder to the guest VM. The first argument is
         # the path on the host to the actual folder. The second argument is
         # the path on the guest to mount the folder. And the optional third
         # argument is a set of non-required options.
         config.vm.synced_folder "C:/Users/wanghuan/Code", "/data"
       
         # Provider-specific configuration so you can fine-tune various
         # backing providers for Vagrant. These expose provider-specific options.
         # Example for VirtualBox:
         #
         config.vm.provider "virtualbox" do |vb|
         #   # Display the VirtualBox GUI when booting the machine
         #   vb.gui = true
         #
         #   # Customize the amount of memory on the VM:
          vb.memory = "2048"
          vb.cpus = 1
          end
         #
         # View the documentation for the provider you are using for more
         # information on available options.
       
         # Enable provisioning with a shell script. Additional provisioners such as
         # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
         # documentation for more information about their specific syntax and use.
         # config.vm.provision "shell", inline: <<-SHELL
         #   apt-get update
         #   apt-get install -y apache2
         # SHELL
       end

       ```
   - 配置git密钥
       ```bash
       # 生成公钥私钥
       ssh-keygen -t rsa -C "lovenico2016@gmail.com"
     
       # 配置git账号与绑定的邮箱
       git config --global user.name "lovenico2016@gmail.com"
       git config --global user.email "Madoka-Kaname"
       ```
   - 启动虚拟机
       ```bash
        vagrant up
       ```

##### 虚拟机的使用

  - 常用vagrant指令
      ```bash
      # 查看虚拟机状态
      vagrant status
    
      # 销毁虚拟机
      vagrant destroy 
    
      # 创建虚拟机
      vagrant up
    
      # 重新加载虚拟机
      vagrant reload 
      
      # 进入虚拟机
      vagrant ssh 
      ```
  - 用户
      ```text
      # vagrant用户和root密码都是vagrant
      # 默认使用vagrant用户登入虚拟机
      # 登入虚拟机后执行su root可切换为root用户
      ```
    
#####  Homestead Box 虚拟机盒子

  - [参考文档](https://learnku.com/courses/laravel-essential-training/5.1/development-environment-windows/148#64f890)
  
  