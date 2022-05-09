---
title: centos安装和使用supervisor
date: 2018-06-21 16:30:32
categories: linux
tags:
- linux
- supervisor
---

##### 简介

> Supervisor是用Python开发的一套通用的进程管理程序，能将一个普通的命令行进程变为后台daemon，并监控进程状态，异常退出时能自动重启。它是通过fork/exec的方式把这些被管理的进程当作supervisor的子进程来启动，这样只要在supervisor的配置文件中，把要管理的进程的可执行文件的路径写进去即可。也实现当子进程挂掉的时候，父进程可以准确获取子进程挂掉的信息的，可以选择是否自己启动和报警。supervisor还提供了一个功能，可以为supervisord或者每个子进程，设置一个非root的user，这个user就可以管理它对应的进程。

##### 名词解释

  ```text
supervisor：要安装的软件的名称。
supervisord：装好supervisor软件后，supervisord用于启动supervisor服务。
supervisorctl：用于管理supervisor配置文件中program。
  ```

##### 安装supervisor
  
  ```bash
  $ sudo su - #切换为root用户
  
  # yum install epel-release
  # yum install -y supervisor
  # systemctl enable supervisord # 开机自启动
  # systemctl start supervisord # 启动supervisord服务
  
  # systemctl status supervisord # 查看supervisord服务状态
  # ps -ef|grep supervisord # 查看是否存在supervisord进程
  ```

##### 配置supervisor

  ```text
[unix_http_server]
file=/tmp/supervisor.sock   ; UNIX socket 文件，supervisorctl 会使用
;chmod=0700                 ; socket 文件的 mode，默认是 0700
;chown=nobody:nogroup       ; socket 文件的 owner，格式： uid:gid

;[inet_http_server]         ; HTTP 服务器，提供 web 管理界面
;port=127.0.0.1:9001        ; Web 管理后台运行的 IP 和端口，如果开放到公网，需要注意安全性
;username=user              ; 登录管理后台的用户名
;password=123               ; 登录管理后台的密码

[supervisord]
logfile=/tmp/supervisord.log ; 日志文件，默认是 $CWD/supervisord.log
logfile_maxbytes=50MB        ; 日志文件大小，超出会 rotate，默认 50MB
logfile_backups=10           ; 日志文件保留备份数量默认 10
loglevel=info                ; 日志级别，默认 info，其它: debug,warn,trace
pidfile=/tmp/supervisord.pid ; pid 文件
nodaemon=false               ; 是否在前台启动，默认是 false，即以 daemon 的方式启动
minfds=1024                  ; 可以打开的文件描述符的最小值，默认 1024
minprocs=200                 ; 可以打开的进程数的最小值，默认 200

; the below section must remain in the config file for RPC
; (supervisorctl/web interface) to work, additional interfaces may be
; added by defining them in separate rpcinterface: sections
[rpcinterface:supervisor]
supervisor.rpcinterface_factory = supervisor.rpcinterface:make_main_rpcinterface

[supervisorctl]
serverurl=unix:///tmp/supervisor.sock ; 通过 UNIX socket 连接 supervisord，路径与 unix_http_server 部分的 file 一致
;serverurl=http://127.0.0.1:9001 ; 通过 HTTP 的方式连接 supervisord

; 包含其他的配置文件
[include]
files = /etc/supervisor/conf.d/*.conf   ; 可以是 *.conf 或 *.ini
;files = relative/directory/*.ini 
  ```

##### 将supervisor配置为开机自启动服务

- 编辑服务文件

  ```bash
  # vim /usr/lib/systemd/system/supervisord.service
  ```
  
- 内容如下

  ```text
    [Unit]
    Description=Supervisor daemon
    
    [Service]
    Type=forking
    PIDFile=/var/run/supervisord.pid
    ExecStart=/bin/supervisord -c /etc/supervisord.conf
    ExecStop=/bin/supervisorctl shutdown
    ExecReload=/bin/supervisorctl reload
    KillMode=process
    Restart=on-failure
    RestartSec=42s
    
    [Install]
    WantedBy=multi-user.target
  ```

##### systemctl管理supervisor

```bash
# systemctl stop supervisord
# systemctl start supervisord
# systemctl status supervisord
# systemctl reload supervisord
# systemctl restart supervisord
# systemctl enable supervisord
# systemctl is-enabled supervisord

```

##### supervisor管理监控的进程

```bash
# 查看监控的进程服务
supervisorctl status
# 重启queue服务
supervisorctl restart queue
# 停止queue服务
supervisorctl stop queue
# 开启queue服务
supervisorctl start queue
```

##### queue配置示例

```text
[program:queue]
command=php think queue:work --queue queue-master --daemon --sleep 2 --tries 3
directory=/data/www/yjy_api/
user=root
stdout_logfile=/data/logs/supervisor/run.log
autostart=true
autorestart=true
startsecs=60
stopasgroup=true
ikillasgroup=true
startretries=1
redirect_stderr=true
```



