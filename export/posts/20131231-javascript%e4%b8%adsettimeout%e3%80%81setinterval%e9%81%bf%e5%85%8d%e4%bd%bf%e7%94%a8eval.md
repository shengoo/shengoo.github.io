title: JavaScript中setTimeout、setInterval避免使用eval()
link: http://www.sheng00.com/1036.html
author: admin
description: 
post_id: 1036
created: 2013/12/31 11:40:54
created_gmt: 2013/12/31 03:40:54
comment_status: open
post_name: javascript%e4%b8%adsettimeout%e3%80%81setinterval%e9%81%bf%e5%85%8d%e4%bd%bf%e7%94%a8eval
status: publish
post_type: post

# JavaScript中setTimeout、setInterval避免使用eval()

定义和用法 setTimeout() 方法用于在指定的毫秒数后调用函数或计算表达式。 setTimeout(code,millisec) //避免使用 setTimeout("myFunc()",1000); //应该用的 setTimeout(myFunc,1000);