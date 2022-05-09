---
title: 解决Centos虚拟机有线网卡消失
date: 2021-03-12 15:19:28
categories: linux
tags:
- linux
- centos
---

> centos系统虚拟机的有线网卡突然消失，导致网络无法连接

<!-- more -->

###### 出现的问题

  - 进入虚拟机，在终端命令`systemctl start network.service`重启网络服务报以下错误(ens33为有线网卡,不同版本可能不同, 如ens32)
   
    ```text  
    Connection 'ens33' is not available on device ens33 because device is strictly unmanaged
    ```


###### 最佳解决

  - 关闭NetworkManager可以起作用，但不推荐，有线网卡消失是因为网卡未加入托管导致，这里重新纳入托管为最佳解决办法。
  
    ```bash
    查看托管状态
    nmcli n
    显示 disabled 则为本文遇到的问题，如果是 enabled 则可以不用往下看了
    开启 托管
    nmcli n on
    重启网络管理
    systemctl restart NetworkManager
    ```