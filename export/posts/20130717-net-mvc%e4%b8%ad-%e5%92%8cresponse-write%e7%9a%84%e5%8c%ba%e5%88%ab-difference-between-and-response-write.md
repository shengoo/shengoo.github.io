title: .net mvc中@ 和response.write的区别 Difference between @ and response.write
link: http://www.sheng00.com/869.html
author: admin
description: 
post_id: 869
created: 2013/07/17 01:18:54
created_gmt: 2013/07/16 17:18:54
comment_status: open
post_name: net-mvc%e4%b8%ad-%e5%92%8cresponse-write%e7%9a%84%e5%8c%ba%e5%88%ab-difference-between-and-response-write
status: publish
post_type: post

# .net mvc中@ 和response.write的区别 Difference between @ and response.write

Razor会自动的将输出进行Html编码，可以帮助防止跨站点攻击。 如果有人将恶意脚本放进数据库，而Razor没有进行Html编码的话，浏览器就会看到一个<script>标签和可执行的JavaScript。