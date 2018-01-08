title: Javascript检测终端浏览器是android或ipad、iphone
link: http://www.sheng00.com/212.html
author: admin
description: 
post_id: 212
created: 2012/01/16 22:08:57
created_gmt: 2012/01/16 14:08:57
comment_status: open
post_name: javascript%e6%a3%80%e6%b5%8b%e6%b5%8f%e8%a7%88%e5%99%a8%e6%98%afandroid%e6%88%96ipad%e3%80%81iphone
status: publish
post_type: post

# Javascript检测终端浏览器是android或ipad、iphone

有些时候会需要判断页面是在哪种移动终端上运行的 `navigator.appVersion: <script>document.write(navigator.appVersion);</script> <br/> Device type: <script>if((/android/gi).test(navigator.appVersion)) document.write("android"); if((/iphone|ipad/gi).test(navigator.appVersion)) document.write("IOS"); </script> <br/>`   navigator.appVersion:    
Device type:    
ps:本文只打印出了是不是android或ios，其他的没有打出来