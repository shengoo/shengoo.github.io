title: C# datetime转换成JavaScript认识的UTC时间
link: http://www.sheng00.com/1013.html
author: admin
description: 
post_id: 1013
created: 2013/12/13 09:58:29
created_gmt: 2013/12/13 01:58:29
comment_status: open
post_name: c-datetime%e8%bd%ac%e6%8d%a2%e6%88%90javascript%e8%ae%a4%e8%af%86%e7%9a%84utc%e6%97%b6%e9%97%b4
status: publish
post_type: post

# C# datetime转换成JavaScript认识的UTC时间

`TimeSpan span = DateTime.Now.Subtract(new DateTime(1970, 1, 1, 0, 0, 0, DateTimeKind.Utc)); Console.WriteLine(span.TotalMilliseconds);` 输出： 1386928595163.35