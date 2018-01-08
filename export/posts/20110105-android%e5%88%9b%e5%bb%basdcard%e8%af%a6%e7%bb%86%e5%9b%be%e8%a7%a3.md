title: Android创建sdcard详细图解
link: http://www.sheng00.com/18.html
author: admin
description: 
post_id: 18
created: 2011/01/05 08:00:00
created_gmt: 2011/01/05 00:00:00
comment_status: open
post_name: android%e5%88%9b%e5%bb%basdcard%e8%af%a6%e7%bb%86%e5%9b%be%e8%a7%a3
status: publish
post_type: post

# Android创建sdcard详细图解

Android应用广泛，应用方式灵活，可以在模拟器中进行相应修改实现许多特定的功能需求。我们在这里就先来了解一下Android创建sdcard的具体方法，从中感受一下这一操作系统的相关特性。

**Android创建sdcard步骤一、cmd进入tools目录输入mksdcard -l mycard 100M F:mysdcard.img**

1\. mycard命令可以使用三种尺寸：字节、K和M。如果只使用数字，表示字节。后面还可以跟K，如262144K，也表示256M。

2\. mycard建立的虚拟文件最小为8M，也就是说，模拟器只支持大于8M的虚拟文件。

3\. -l命令行参数表示虚拟磁盘的卷标，可以没有该参数。

4\. 虚拟文件的扩展名可以是任意的，如mycard.abc。

5\. mksdcard命令不会自动建立不存在的目录，因此，在执行上面命令之前，要先在当前目录中建立一个card目录。

6\. mksdcard命令是按实际大小生成的sdcard虚拟文件。也就是说，生成256M的虚拟文件的尺寸就是256M，如果生成较大的虚拟文件，要看看自己的硬盘空间够不够哦！

**Android创建sdcard步骤二、激活sdcard**

1.命令行输入：emulator -avd my_android1.5 -sdcard F:mysdcard.img

我在命令行输入激活不了，不知为什么！待解决！

emulator: ERROR: the user data image is used by another emulator. aborting

2.如果在开发环境（Eclipse）中，可以在Run Configuration对话框中设置启动参数

![](/wp-content/uploads/2013/06/cc2c_65a251cfaeeef772f9dc617c.jpg)

或者在Preferences-->Android-->Launch加入

![](/wp-content/uploads/2013/06/20bd_9758be3d6ff5b94fbba1677c.jpg)

**Android创建sdcard步骤三、sdcard中加入内容**

F:android-sdk-windows-1.5_r3tools>adb push E:Xunleigive.mp3 /sdcard/give.mp3