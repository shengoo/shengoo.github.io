title: wordpress搬家到cPanel主机
link: http://www.sheng00.com/232.html
author: admin
description: 
post_id: 232
created: 2012/01/16 22:43:01
created_gmt: 2012/01/16 14:43:01
comment_status: open
post_name: wordpress%e6%90%ac%e5%ae%b6%e5%88%b0cpanel%e4%b8%bb%e6%9c%ba
status: publish
post_type: post

# wordpress搬家到cPanel主机

之前备份了数据库sql文件和整站的文件，考虑已久决定的事情当然早有准备。 搬家过程如下： 1.还原数据库和wordpress文件 登陆cPanel管理页面创建新的数据库 ![2012-01-16_22-31-37](/wp-content/uploads/2012/01/2012-01-16_22-31-37_thumb.jpg) 然后添加mysql用户向刚才建立的数据库添加这个用户，记下用户名和密码，等下要在原先的wordpress的wp-config.php里修改数据库和用户名 ![2012-01-16_22-33-34](http://www.sheng00.com/wp-content/uploads/2012/01/2012-01-16_22-33-34_thumb.jpg)   之前备份的wordpress文件压缩成rar格式的，结果传到cPanel上不能解压缩，又换成zip格式的传上去解了压缩 2.修改wp-config.php指向新的数据库 找到wp-config.php右击选择Edit ![2012-01-16_22-38-00](http://www.sheng00.com/wp-content/uploads/2012/01/2012-01-16_22-38-00_thumb.jpg) 然后编辑你的数据库配置 ![2012-01-16_22-39-32](http://www.sheng00.com/wp-content/uploads/2012/01/2012-01-16_22-39-32_thumb.jpg) 然后就大功告成了，   如果你的域名变了的话，就要进mysql里的wp_options表里改下siteurl和host的值 大功告成，搬家成功！