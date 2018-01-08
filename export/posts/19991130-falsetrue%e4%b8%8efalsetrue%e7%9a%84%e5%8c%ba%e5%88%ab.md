title: FALSE/TRUE与false/true的区别
link: http://www.sheng00.com/85.html
author: admin
description: 
post_id: 85
created: 1999/11/30 08:00:00
created_gmt: 1999/11/30 00:00:00
comment_status: open
post_name: falsetrue%e4%b8%8efalsetrue%e7%9a%84%e5%8c%ba%e5%88%ab
status: publish
post_type: post

# FALSE/TRUE与false/true的区别

1.FALSE/TRUE与false/true的区别：  
false/true是标准C++语言里新增的关键字，而FALSE/TRUE是通过#define，这要用途  
是解决程序在C与C++中环境的差异,以下是FALSE/TRUE在windef.h的定义：  
#ifndef FALSE  
#define FALSE 0  
#endif  
#ifndef TRUE  
#define TRUE 1  
#endif  
也就是说FALSE/TRUE是int类型，而false/true是bool类型；所以两者不一样的，只不过  
我们在使用中没有这种感觉，因为C++会帮你做隐式转换。  
2.bool的大小与BOOL的区别：  
bool在C++里是占用1字节,而BOOL是int类型，int类型的大小是视具体环境而定的；所以  
来说：false/true只占用1个字节,而TRUE/FALSE视具体环境而言，以下是BOOL在windef  
.h中的定义：typedef int BOOL;  
3.NULL与0的区别：  
还是让我们看一下windef.h中NULL的定义：  
#ifndef NULL  
#ifdef __cplusplus//这个是指示是用C++来编译程序  
#define NULL 0  
#else  
#define NULL ((void *)0)  
#endif  
#endif  
所以说：它们没有区别，只不过在C里面会做一个强制类型转换。