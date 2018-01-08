title: Node.js使用express处理静态文件，static file
link: http://www.sheng00.com/980.html
author: admin
description: 
post_id: 980
created: 2013/10/16 14:35:59
created_gmt: 2013/10/16 06:35:59
comment_status: open
post_name: node-js%e4%bd%bf%e7%94%a8express%e5%a4%84%e7%90%86%e9%9d%99%e6%80%81%e6%96%87%e4%bb%b6%ef%bc%8cstatic-file
status: publish
post_type: post

# Node.js使用express处理静态文件，static file

var express = require('express');
    var app = express();
    
    // log requests
    app.use(express.logger('dev'));
    
    app.use(express.static(__dirname + '/public'));
    
    app.listen(1024);
    console.log('Listening on port 1024');
    

使用http://localhost:1024/css/style.css就可以读取/public/css/style.css文件了