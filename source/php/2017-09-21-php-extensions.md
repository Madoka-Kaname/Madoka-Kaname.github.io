---
title: php扩展库安装
date: 2017-09-21 11:34:20
categories: php
tags:
- php
---

<!-- more -->

### windows环境下PHP安装扩展

  - 通过phpinfo()函数，进行查看扩展是否已安装
  
      ```php
    <?php
        echo phpinfo();
    ?>
      ```
    
  - 根据php版本前往官方网址下载对应的扩展库
    
    [下载地址](http://pecl.php.net/packages.php)
    
    windows对应`dll`， nts非线程安全，ts线程安全，x64代表64位，x86代表32位。
    
  - 将下载的扩展库文件放入对应的扩展库文件夹，修改php.ini, 以下以redis为例
  
    ```text
    extension=php_igbinary.dll
    extension=php_redis.dll
    ``` 
    
### linux(centos/redhat)环境下PHP安装扩展

###### 方法一: 源码安装

1. 下载php版本对应的扩展源码包

    - 例如redis
    
      `http://pecl.php.net/package/redis`

2. 解压进入源码目录

    ```bash
    $ tar -zxvf redis.tar.gz
   
    $ cd redis
   
    $ /usr/bin/phpize 
   
    $ ./configure --with-php-config=/usr/bin/php-config
   
    $ make && make install
   
    $ echo "extension=redis.so" >> /etc/php.ini
    
    ```
   
###### 方法二: pecl扩展库安装

- 终端执行指令
    
    ```bash
    $ pecl install -o -f redis 
  
    $ echo "extension=redis.so" >> /etc/php.ini
  
    ```