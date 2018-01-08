title: 让很多Promise一个接一个进行
link: http://www.sheng00.com/2190.html
author: admin
description: 
post_id: 2190
created: 2017/12/01 22:12:12
created_gmt: 2017/12/01 14:12:12
comment_status: open
post_name: %e8%ae%a9%e5%be%88%e5%a4%9apromise%e4%b8%80%e4%b8%aa%e6%8e%a5%e4%b8%80%e4%b8%aa%e8%bf%9b%e8%a1%8c
status: publish
post_type: post

# 让很多Promise一个接一个进行

Promise是我们处理异步操作的时候经常用到的。 有的时候我们会需要顺序执行很多异步操作，如果操作比较少的时候还可以写成`a.then(b).then(c)...`,可是如果异步操作很多的时候就不能这样写了。 可以利用数组的reduce函数达到同样的效果，这个时候不管有多少异步操作都可以连在一起了。 代码如下： 
    
    
    function waitPromise(time) {
        console.log(time);
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                resolve('resolved');
            }, time);
        });
    }
     
    function log(data) {
        return new Promise((resolve, reject) => {
            console.log(data + '@' + (new Date().getSeconds()));
            resolve();
        });
    }
     
    var ps = [];
    for (var i = 0; i < 3; i++) {
        let time = (i + 1) * 1000;
        ps.push(() => waitPromise(time));
        ps.push(log);
    }
     
     
    console.log('started' + '@' + (new Date().getSeconds()));
    var p = Promise.resolve();
    ps.reduce((p, c) => {
        return p.then(c)
    }, p).then(() => {
        console.log('all finished');
    }).catch(reject => {
        console.log('reject', reject)
    });

输出结果: 
    
    
    started@59
    1000
    resolved@0
    2000
    resolved@2
    3000
    resolved@5
    all finished