title: npm设置代理
link: http://www.sheng00.com/1085.html
author: admin
description: 
post_id: 1085
created: 2014/03/20 12:12:53
created_gmt: 2014/03/20 04:12:53
comment_status: open
post_name: npm%e8%ae%be%e7%bd%ae%e4%bb%a3%e7%90%86
status: publish
post_type: post

# npm设置代理

### 无密码的：
    
    
    $ npm config set proxy http://server:port
    $ npm config set https-proxy http://server:port
    

### 有密码的
    
    
    $ npm config set proxy http://username:password@server:port
    $ npm config set https-proxy http://username:pawword@server:port
    

### 删除代理
    
    
    npm config rm proxy
    npm config rm https-proxy