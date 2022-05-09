---
title: github加速
date: 2019-01-12 12:49:26
categories: github
tags:
- github
---

> github

### 问题

  众所周知的原因，github服务器在国外，因为墙的原因，获取包的时候，所以需要配置代理服务。

### 代理加速
  
  - 梯子一个
  - 配置http协议代理
    
    ```bash
    # 为全局的 git 项目都设置代理(192.168.0.88:7078为代理服务地址)
    git config --global http.proxy 192.168.0.88:7078
    
    # 为某个 git 项目单独设置代理
    git config --local http.proxy 192.168.0.88:7078
    
    # 取消代理
    git config --global --unset http.proxy
    ```
  
  - 另外还有`https`和`socks5`协议的代理, 方法类似.
  









    