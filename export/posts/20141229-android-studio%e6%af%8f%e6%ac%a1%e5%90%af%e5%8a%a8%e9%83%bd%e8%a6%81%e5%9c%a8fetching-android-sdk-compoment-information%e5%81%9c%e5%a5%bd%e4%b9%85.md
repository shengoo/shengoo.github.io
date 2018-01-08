title: android studio每次启动都要在fetching Android sdk compoment information停好久
link: http://www.sheng00.com/2006.html
author: admin
description: 
post_id: 2006
created: 2014/12/29 20:15:53
created_gmt: 2014/12/29 12:15:53
comment_status: open
post_name: android-studio%e6%af%8f%e6%ac%a1%e5%90%af%e5%8a%a8%e9%83%bd%e8%a6%81%e5%9c%a8fetching-android-sdk-compoment-information%e5%81%9c%e5%a5%bd%e4%b9%85
status: publish
post_type: post

# android studio每次启动都要在fetching Android sdk compoment information停好久

网上有人给出了方案： 1）进入刚安装的Android Studio目录下的bin目录。找到idea.properties文件，用文本编辑器打开。 2）在idea.properties文件末尾添加一行： disable.android.first.run=true ，然后保存文件。 3）关闭Android Studio后重新启动，便可进入界面。