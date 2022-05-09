---
title: go lang入门
date: 2017-04-19 12:39:26
categories: go lang
tags:
- go lang
---

> go

### 快速入门
  
  - [《The Go Programming Language》中文web版](http://books.studygolang.com/gopl-zh/)
  
  - [《Go Web 编程》中文web版](https://astaxie.gitbooks.io/build-web-application-with-golang/content/zh/01.1.html)

### centos7环境标准包方式安装和配置

  - 如果系统是64,下载64位标准包,否则如果是32位,那么就下载32位标准包。

    ```bash
    curl -O https://golang.org/dl/
    ```
    
  - 解压到安装目录, 如安装到/usr/local目录下
  
    ```bash
    tar zvxf go1.16.3.linux-amd64.tar.gz -C /usr/local/
    ```

  - 配置环境变量
  
    - 打开环境变量配置文件
    
      ```bash
      vim /etc/profile
      ```
      
    - 添加配置内容如下(具体的安装目录和工作目录以自己实际的为准)
    
      ```text
        export GOROOT=/usr/local/go
        export GOPATH=/var/www/core/go_work
        export GOBIN=$GOROOT/bin
        export PATH=$GOROOT/bin:$GOPATH/bin
      ```
    
    - 重新编译加载配置
    
      ```bash
      source /etc/profile
      ```
      
    - 查看`go env` 和 `go --version`, 看看配置是否生效







