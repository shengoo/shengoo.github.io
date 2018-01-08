title: 判断当前的JavaScript是否开启了“use strict”模式,JavaScript check if strict mode is enforced?
link: http://www.sheng00.com/2037.html
author: admin
description: 
post_id: 2037
created: 2015/01/06 11:42:41
created_gmt: 2015/01/06 03:42:41
comment_status: open
post_name: %e5%88%a4%e6%96%ad%e5%bd%93%e5%89%8d%e7%9a%84javascript%e6%98%af%e5%90%a6%e5%bc%80%e5%90%af%e4%ba%86use-strict%e6%a8%a1%e5%bc%8fjavascript-check-if-strict-mode-is-enforced
status: publish
post_type: post

# 判断当前的JavaScript是否开启了“use strict”模式,JavaScript check if strict mode is enforced?

使用以下代码可以判断是否开启了strict模式 
    
    
    var isStrict = (function () { return !this; })();  
    console.log(isStrict); 
    

因为在strict模式下，上面函数里的this是undefined 而在非strict模式下，上面函数里的this是Window（如果在浏览器里运行）或者其他运行环境，比如node等