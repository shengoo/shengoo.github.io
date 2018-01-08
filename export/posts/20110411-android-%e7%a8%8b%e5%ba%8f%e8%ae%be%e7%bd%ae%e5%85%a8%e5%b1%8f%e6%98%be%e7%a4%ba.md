title: android 程序设置全屏显示
link: http://www.sheng00.com/10.html
author: admin
description: 
post_id: 10
created: 2011/04/11 08:00:00
created_gmt: 2011/04/11 00:00:00
comment_status: open
post_name: android-%e7%a8%8b%e5%ba%8f%e8%ae%be%e7%bd%ae%e5%85%a8%e5%b1%8f%e6%98%be%e7%a4%ba
status: publish
post_type: post

# android 程序设置全屏显示

2中方法

 

在AndroidManifest.xml中

<activity android:name=""  
  
...  
  
android:theme="@android:style/Theme.NoTitleBar.Fullscreen"/>

 

程序里

@Override  
public void onCreate(Bundle savedInstanceState) {  
    super.onCreate(savedInstanceState);  
    requestWindowFeature(Window.FEATURE_NO_TITLE);  
    getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN, WindowManager.LayoutParams.FLAG_FULLSCREEN);  
...