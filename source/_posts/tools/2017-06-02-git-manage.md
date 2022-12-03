---
title: git版本管理工具
date: 2017-06-02 12:39:26
categories: tools
tags:
- git
- tools
---

> git

##### 搭建git服务
  
##### 安装git客户端
  - 在centos系统
      ```bash
      yum install git
      git --version
      ```
    
##### git指令
  - 常用
      ```bash
      # 拉取远程仓库代码(默认分支)
      git clone git@github.com:Madoka-Kaname/Madoka-Kaname.github.io.git
    
      # 拉取远程仓库指定分支
      git checkout -b main origin/main
      
      # 推送远程仓库指定分支
      # git push origin main
    
      # 强行推送远程仓库
      # git push --force origin main
    
      # 显示所有远程仓库包括url
      git remote -v
      ```
      # 查看提交信息
      git log 
      
      # 默认推送方式
      git config --global push.default matching
      
      # 拉取分支
      git pull --rebase origin master
      
      # 强推分支
      git push -u origin master

##### 开发工作流

  - merge方式
  
    优点:方便管理, 安全性高, 可追溯, 适合小团队
    缺点:步骤繁琐, 结构复杂, 过多的合并线, 不易代码审查
    
      ```bash
      # 合并master到feature分支
      git checkout feature
      git merge master 
      
      # 或者
      git merge feature master
      ```
    
  - rebase方式
  
    优点:结构清晰, 方便代码审查, 适合大团队
    缺点:需要合理管理, 不遵守rebase的黄金法则容易丢失了合并提交能够提供的上下文信息
  
      ```bash
      # 把feature分支的提交历史rebase到main分支的提交历史顶端
      git checkout feature
      git rebase main
    
      # 可交互式rebase
      git checkout feature
      git rebase -i main
        执行以上命令会打开一个文本编辑器，其中内容为分支中需要移动的所有提交列表
      pick 33d5b7a Message for commit #1
      pick 9480b3d Message for commit #2
      pick 5c67e61 Message for commit #3
        使用fixup命令替代pick来把两次提交压缩在一起
      pick 33d5b7a Message for commit #1
      fixup 9480b3d Message for commit #2
      pick 5c67e61 Message for commit #3
        保存并关闭这个文件之后，Git会根据你的调改结果执行rebase操作
    
      # rebase操作黄金法则:永远不要在公共分支上使用它
      ```
    
##### 参考来源
  - [git工作流](https://www.zhihu.com/question/36509119/answer/2423381574)
  
  
  







