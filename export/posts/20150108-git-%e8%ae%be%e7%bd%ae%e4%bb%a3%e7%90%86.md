title: Git 设置代理
link: http://www.sheng00.com/2044.html
author: admin
description: 
post_id: 2044
created: 2015/01/08 20:01:13
created_gmt: 2015/01/08 12:01:13
comment_status: open
post_name: git-%e8%ae%be%e7%bd%ae%e4%bb%a3%e7%90%86
status: publish
post_type: post

# Git 设置代理

可以使用命令行设置，也可以通过配置文件设置。 

## 使用命令行

### 设置代理
    
    
    git config --global http.proxy http://proxyuser:proxypwd@proxy.server.com:8080
    git config --global https.proxy https://proxyuser:proxypwd@proxy.server.com:8080
    

  * `proxyuser` 是你代理服务器的用户名
  * `proxypwd` 是你代理服务器用户名的密码
  * `proxy.server.com` 是你代理服务器的地址，直接写ip也可以
  * `8080` 代理服务器的端口

### 删除代理
    
    
    git config --global --unset http.proxy
    git config --global --unset https.proxy
    

## 使用配置文件

在你的用户的根目录下，有个文件`.gitconfig`,可以通过更改这个文件来设置代理 增加以下代码： 
    
    
    [http]
        proxy = http://username:password@proxy.at.your.org:8080
    

### mac

![mac.gitconfig](/wp-content/uploads/2015/01/mac.gitconfig.png)

### ubuntu

![ubuntu.gitconfig](/wp-content/uploads/2015/01/ubuntu.gitconfig.png)

### windows

![image 1420765034](/wp-content/uploads/2015/01/image-1420765034.png)