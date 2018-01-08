title: 关于Linux下C/C++程序编译
link: http://www.sheng00.com/90.html
author: admin
description: 
post_id: 90
created: 1999/11/30 08:00:00
created_gmt: 1999/11/30 00:00:00
comment_status: open
post_name: %e5%85%b3%e4%ba%8elinux%e4%b8%8bcc%e7%a8%8b%e5%ba%8f%e7%bc%96%e8%af%91
status: publish
post_type: post

# 关于Linux下C/C++程序编译

在编译之前我们需要在系统里安装G++ GCC，它们就是Linux下的C++/C的编译器。代码如下   
代码:   
  
sudo apt-get install build-essential   
  
好，现在我们在文本编辑器里写一个C的简单的程序（好像所有学习C或者C++的书都会出现）   
代码:   
  
＃include <stdio.h>   
int main()   
{   
printf("Hello,World!n");   
return 0;   
}   
  
现在存盘为Hello.c，打开你的终端，并在文件当前目录输入：   
代码:   
  
gcc Hello.c -o hello      
  
编译时可能会出现如下警告：no newline at and of file ，只有在文件结尾添加一个新行就好了。   
然后在终端中输入 ./hello ，你就能在终端中看到程序运行结果了。   
  
下面来说下C++是如何编译的   
写程序（不用我多说了吧）   
代码:   
  
#include <iostream>   
using namespace std;   
int main()   
{   
cout<<"Hello,World!n"<<endl;   
return 0;   
}   
  
存盘为Hello.cpp   
使用gcc编译？？？ 不对，这里我们使用g++来编译C++程序   
代码:   
  
g++ Hello.cpp -o hello   
  
  
编译多个文件我们怎么办？？？ 来看下面出了三个文件Hello.h, Hello.cpp, MyFirst.cpp   
代码:   
  
//file_NO1:Hello.h   
class Hello {   
Hello();   
void Display();   
}   
//file_NO2:Hello.cpp   
#include <iostream>   
#include "Hello.h"   
using namespace std;   
Hello::Hello()   
{   
}   
Hello::Display()   
{   
cout<<"Hello,World!n"<<endl;   
}   
//file_NO3:MyFirst.cpp   
#include <iostram>   
#include "Hello.cpp"   
int main()   
{   
Hello theHello;   
theHello->Display();   
return 0;   
}   
  
在g++中有一个参数-c 可以只编译不连接，那么我们就可以按如下顺序编译文件，   
代码:   
  
g++ -c Hello.cpp -o Hello.o   
g++ -c MyFirst.cpp -o MyFirst.o   
g++ MyFirst.o hello.o -o MyFirst   
  
你是否会问，如果是一个项目的话，可能会有上百个文件，这样的编译法，人不是要累死在电脑前吗，或者等到你编译成功了，岂不是头发都白了，呵呵，所以我们要把上述的编译过程写进以下一个文本文件中：   
Linux下称之为makefile   
[code]   
#这里可以写一些文件的说明   
MyFirst: MyFirst.o hello.o   
g++ MyFirst.o hello.o -o MyFirst   
Hello.o:Hello.cpp   
g++ -c Hello.cpp -o Hello.o   
MyFirst.o:MyFirst.cpp   
g++ -c MyFirst.cpp -o MyFirst.o   
[code]   
存盘为MyFirst，在终端输入：make MyFist ，程序出现了错误可是所有程序员共同的敌人，在编写程序时我们应该尽量的去避免错误 的出现，不过编写的时候再怎么都不可避免的出现这样那样的错误，对程序进行必要的调试是一个好主意，那我们怎么来调试程序呢，看下面：   
[code]   
gdb ./文件名   
[/code]   
以下为调试状态下的可以用到的命令（可以仅输入单词的输入，如break可简为b），尖括号中为说明   
[code]   
list <显示源代码>   
break 行号 <设置断点>   
run <运行程序>   
continue <继续从断点处执行>   
print 变量 <调试时查看变量的值>   
del 行号 <删除断点>   
step <单步执行，可跟踪到函数内部>   
next <单步执行，不可跟踪到函数内部>   
quit <退出>   
[/code]