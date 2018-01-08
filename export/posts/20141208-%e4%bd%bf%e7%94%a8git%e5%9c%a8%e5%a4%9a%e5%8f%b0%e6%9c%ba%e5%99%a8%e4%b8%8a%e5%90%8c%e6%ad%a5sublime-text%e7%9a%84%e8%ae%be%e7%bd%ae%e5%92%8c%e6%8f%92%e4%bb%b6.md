title: 使用git在多台机器上同步sublime text的设置和插件
link: http://www.sheng00.com/1861.html
author: admin
description: 
post_id: 1861
created: 2014/12/08 13:45:53
created_gmt: 2014/12/08 05:45:53
comment_status: open
post_name: %e4%bd%bf%e7%94%a8git%e5%9c%a8%e5%a4%9a%e5%8f%b0%e6%9c%ba%e5%99%a8%e4%b8%8a%e5%90%8c%e6%ad%a5sublime-text%e7%9a%84%e8%ae%be%e7%bd%ae%e5%92%8c%e6%8f%92%e4%bb%b6
status: publish
post_type: post

# 使用git在多台机器上同步sublime text的设置和插件

### package文件夹位置

windows: `C:\Users\\[YourName]\AppData\Roaming\Sublime Text 3\Packages` mac: `/Library/Application\ Support/Sublime\ Text\ 3/Packages/` linux: 

### 有些文件/文件夹不需要同步，加入到.gitignore
    
    
    Package Control.last-run
    Package Control.ca-list
    Package Control.ca-bundle
    Package Control.system-ca-bundle
    Package Control.cache/
    Package Control.ca-certs/

### 在第一台电脑上
    
    
    cd [package folder]/User/
    git init
    git add
    git commit -m "Initial"
    git remote add origin [your git repo]
    git push origin master

### 这样就可以在其他电脑上clone这个repo了
    
    
    cd [package folder]
    mv User User.old
    git clone [your git repo] User

### 如果设置有了改变，再同步到repo里
    
    
    cd [package folder]/User
    git add -A
    git commit -m "Update settings"
    git push

### 在其他电脑上同步
    
    
    cd [package folder]/User
    git pull