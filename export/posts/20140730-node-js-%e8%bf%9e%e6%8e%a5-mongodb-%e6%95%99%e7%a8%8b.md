title: Node.js 连接 mongodb 教程
link: http://www.sheng00.com/1248.html
author: admin
description: 
post_id: 1248
created: 2014/07/30 15:55:55
created_gmt: 2014/07/30 07:55:55
comment_status: open
post_name: node-js-%e8%bf%9e%e6%8e%a5-mongodb-%e6%95%99%e7%a8%8b
status: publish
post_type: post

# Node.js 连接 mongodb 教程

新建一个文件夹存放我们的js文件 1.package.json 使用mongodb 
    
    
    {
      "name": "test",
      "version": "0.0.1",
      "private": true,
      "scripts": {
      "start": "node app.js"
      },
      "dependencies": {
      "mongodb":"1.4.7"
      }
    }

2.创建文件mongo.js 
    
    
    var MongoClient = require('mongodb').MongoClient;
    var db;
    var connected = false;
    
    module.exports = {
      connect: function(url, callback){
      MongoClient.connect(url, function(err, _db){
        if (err) { throw new Error('Could not connect: '+err); }
    
        db = _db;
        connected = true;
    
        callback(db);
        });
      },
      collection: function(name){
        if (!connected) {
        throw new Error('Must connect to Mongo before calling "collection"');
        }
    
        return db.collection(name);
      }
    };
    

3.创建app.js 
    
    
    var mongo = require('./mongo');
    
    var mongoUrl = "mongodb://localhost:27017/test";
    mongo.connect(mongoUrl, function(){
    console.log('Connected to mongo at: ' + mongoUrl);
    var coll = mongo.collection('users');
    
    var userObject = {
      username: "admin",
      password: "admin"
    };
    
    // create the new user
    coll.insert(userObject, function(err,user){
      console.log("created user");
    });
    
    coll.find().toArray(function(err, results) {
      console.dir(results);
      });
    });

  源码下载：https://github.com/shengoo/mongotest 效果如下： ![mongodb test](/wp-content/uploads/2014/07/Untitled.png)