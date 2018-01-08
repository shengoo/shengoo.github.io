title: JavaScript原型继承
link: http://www.sheng00.com/1397.html
author: admin
description: 
post_id: 1397
created: 2014/08/24 22:21:14
created_gmt: 2014/08/24 14:21:14
comment_status: open
post_name: javascript%e5%8e%9f%e5%9e%8b%e7%bb%a7%e6%89%bf
status: publish
post_type: post

# JavaScript原型继承

function A(){
      this.fa = function(){
        console.log("function in A");
      }
    }
    
    function B(){
      this.fb = function(){
        console.log("function in B");
      }
    }
    
    var a = new A();
    a.fa();//function in A
    
    var b = new B();
    // b.fa(); //throw error;
    b.fb(); //function in B
    console.log(b instanceof A) //false
    
    B.prototype = new A();
    var b = new B();
    b.fa(); //function in A
    b.fb(); //function in B
    console.log(b instanceof A)//true
    console.log(b instanceof B)//true