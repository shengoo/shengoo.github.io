title: Node.js使用express解析cookie
link: http://www.sheng00.com/985.html
author: admin
description: 
post_id: 985
created: 2013/10/16 23:36:33
created_gmt: 2013/10/16 15:36:33
comment_status: open
post_name: node-js%e4%bd%bf%e7%94%a8express%e8%a7%a3%e6%9e%90cookie
status: publish
post_type: post

# Node.js使用express解析cookie

首先使用cookieParser()解析请求头里的Cookie, 并用cookie名字的键值对形式放在 req.cookies 你也可以通过传递一个secret 字符串激活签名了的cookie 。 `app.use(express.cookieParser()); app.use(express.cookieParser('some secret')); ` 下面是读写cookie的代码 
    
    
    var express = require('express');
    var app = express();
    
    app.get('/readcookie',function(req,res){
        res.send('req.cookies.name:' + req.cookies.name);
    });
    
    app.get('/writecookie',function(req,res){
        res.cookie('name', 'I'm a cookie', 60000);
        res.send("cookie saved");
    });
    
    app.listen(3000);
    console.log('listening on port 3000');