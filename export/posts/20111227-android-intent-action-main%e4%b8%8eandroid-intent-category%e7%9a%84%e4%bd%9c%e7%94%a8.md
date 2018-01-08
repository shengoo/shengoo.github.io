title: android.intent.action.MAIN与android.intent.category的作用
link: http://www.sheng00.com/193.html
author: admin
description: 
post_id: 193
created: 2011/12/27 10:57:40
created_gmt: 2011/12/27 02:57:40
comment_status: open
post_name: android-intent-action-main%e4%b8%8eandroid-intent-category%e7%9a%84%e4%bd%9c%e7%94%a8
status: publish
post_type: post

# android.intent.action.MAIN与android.intent.category的作用

在android和ophone的应用程序可以有多个Activity，每个Activity是同级别的，那么在启动程序时，最先启动哪个Activity呢？

有些程序可能需要显示在程序列表里，有些不需要。怎么定义呢？

android.intent.action.MAIN决定应用程序最先启动的Activity 。   
android.intent.category.LAUNCHER决定应用程序是否显示在程序列表里。

因为你的程序可能有很多个activity，   
只要xml配置文件中有这么一个intent-filter，而且里面有这个launcher，那么这个activity就是点击程序时最先运行的那个activity。

如果只有一个Activity，没有这两句也可以。