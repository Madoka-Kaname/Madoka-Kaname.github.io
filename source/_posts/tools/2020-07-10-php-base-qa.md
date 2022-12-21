---
title: php基础面试题整理
date: 2020-07-10 12:39:26
categories: php
tags:
- php
---

##### 语法部分

- isset()和empty区别
  ```text
    isset检查变量是否存在且不为NULL, empty()检查一个变量是否为空.
    isset检查值为NULL的变量为false, empty检查为0相关的变量为false.
  ```
  
- error_reporting作用
  ```text
    设置当前程序的错误报告级别
  ```
  
- session和cookie区别
  ```text
    都是用于跟踪用户的整个会话, SESSION存储在服务器端, COOKIE保存在客户端, SESSION相对来说更安全.
  ```
  
- get和post区别
  ```text
    GET是通过URL传递参数的, 只能进行URL编码, GET传送的参数长度也是有限制, 不适合传递敏感数据.
    POST是通过REQUEST BODY传递参数, 支持多种编码方式, 对参数长度没有限制, 对传递的参数数据类型没有限制.
  ```

- include和require区别
  ```text
    include加载脚本文件不存在时不会报错, require会报致命错误, 中断程序, 有once后缀的会判断当前载入的脚本文件是否已经载入过, 如果载入了就不再执行.
  ```