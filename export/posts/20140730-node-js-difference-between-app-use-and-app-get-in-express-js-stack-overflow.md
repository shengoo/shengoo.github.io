title: node.js - Difference between app.use and app.get in express.js
link: http://www.sheng00.com/1258.html
author: admin
description: 
post_id: 1258
created: 2014/07/30 17:43:04
created_gmt: 2014/07/30 09:43:04
comment_status: open
post_name: node-js-difference-between-app-use-and-app-get-in-express-js-stack-overflow
status: publish
post_type: post

# node.js - Difference between app.use and app.get in express.js

[http://stackoverflow.com/questions/15601703/difference-between-app-use-and-app-get-in-express-js](http://expressjs.com/api.html#app.use)

`app.use() `is intended for binding [middleware](http://expressjs.com/api.html#middleware) to your application. The `path` is a "_mount_" or "_prefix_" path and limits the middleware to only apply to any paths requested that **begin** with it. It can even be used to embed another application: 
    
    
    // subapp.js
    var express = require('express');
    var app = modules.exports = express();
    // ...
    
    
    
    // server.js
    var express = require('express');
    var app = express();
    
    app.use('/subapp', require('./subapp'));
    
    // ...
    

By specifying / as a "mount" path, app.use() will respond to any path that starts with /, which are all of them and regardless of HTTP verb used: GET / PUT /foo POST /foo/bar etc. app.get(), on the other hand, is part of Express' application routing and is intended for matching and handling a specific route when requested with the GET HTTP verb: GET / And, the equivalent routing for your example of app.use() would actually be: 
    
    
    app.all(/^/.*/, function (req, res) {
        res.send('Hello');
    });