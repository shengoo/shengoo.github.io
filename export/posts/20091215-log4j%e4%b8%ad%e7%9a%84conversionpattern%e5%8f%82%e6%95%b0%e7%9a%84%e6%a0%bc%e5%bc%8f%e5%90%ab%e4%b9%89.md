title: log4j中的ConversionPattern参数的格式含义
link: http://www.sheng00.com/33.html
author: admin
description: 
post_id: 33
created: 2009/12/15 08:00:00
created_gmt: 2009/12/15 00:00:00
comment_status: open
post_name: log4j%e4%b8%ad%e7%9a%84conversionpattern%e5%8f%82%e6%95%b0%e7%9a%84%e6%a0%bc%e5%bc%8f%e5%90%ab%e4%b9%89
status: publish
post_type: post

# log4j中的ConversionPattern参数的格式含义

格式名 含义   
%c 输出日志信息所属的类的全名   
%d 输出日志时间点的日期或时间，默认格式为ISO8601，也可以在其后指定格式，比如：%d{yyy-MM-dd HH:mm:ss }，输出类似：2002-10-18- 22：10：28   
%f 输出日志信息所属的类的类名   
%l 输出日志事件的发生位置，即输出日志信息的语句处于它所在的类的第几行   
%m 输出代码中指定的信息，如log(message)中的message   
%n 输出一个回车换行符，Windows平台为“rn”，Unix平台为“n”   
%p 输出优先级，即DEBUG，INFO，WARN，ERROR，FATAL。如果是调用debug()输出的，则为DEBUG，依此类推   
%r 输出自应用启动到输出该日志信息所耗费的毫秒数   
%t 输出产生该日志事件的线程名