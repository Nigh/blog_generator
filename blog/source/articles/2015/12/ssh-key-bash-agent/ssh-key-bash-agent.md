title: 在bash中添加ssh key for git
date: 2015-12-07 17:00:00 +0800
author: me
cover: 
draft: true
tags:
    - code
preview: 

---

1. 设置git的`user.name`和`user.email`
2. 生成ssh密钥`ssh-keygen -t rsa -C "your email"`
3. 将生成的公钥按需添加至目标
4. 使用`ssh-add 私钥路径`添加私钥
5. 在上一步中若出现这个错误:`Could not open a connection to your authentication agent`，则执行`ssh-agent bash`可以解决