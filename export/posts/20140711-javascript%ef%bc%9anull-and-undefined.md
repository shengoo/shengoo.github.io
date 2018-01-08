title: javascript：null and undefined
link: http://www.sheng00.com/1182.html
author: admin
description: 
post_id: 1182
created: 2014/07/11 13:56:27
created_gmt: 2014/07/11 05:56:27
comment_status: open
post_name: javascript%ef%bc%9anull-and-undefined
status: publish
post_type: post

# javascript：null and undefined

声明而没有赋值的变量是undefined 没有返回值的函数返回的是undefined `
    
    
    var a;//undefined
    console.log(a);//undefined
    console.log(typeof a);//undefined
    console.log(typeof a == undefined)//false
    console.log(typeof a == "undefined")//true
    console.log(typeof a === undefined)//false
    console.log(typeof a === "undefined")//true
    console.log(a==null);//true
    console.log(a==undefined);//true
    console.log(a===null);//false
    console.log(a===undefined);//true
    
    
    console.log("*******************");
    
    var b = null;//null
    console.log(b);//null
    console.log(typeof b);//object
    console.log(typeof b == undefined)//false
    console.log(typeof b == "undefined")//false
    console.log(typeof b === undefined)//false
    console.log(typeof b === "undefined")//false
    console.log(b==null);//true
    console.log(b==undefined);//true
    console.log(b===null);//true
    console.log(b===undefined);//false

`