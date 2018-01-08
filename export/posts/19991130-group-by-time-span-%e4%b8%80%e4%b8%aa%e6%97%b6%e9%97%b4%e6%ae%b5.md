title: group by time span  一个时间段
link: http://www.sheng00.com/53.html
author: admin
description: 
post_id: 53
created: 1999/11/30 08:00:00
created_gmt: 1999/11/30 00:00:00
comment_status: open
post_name: group-by-time-span-%e4%b8%80%e4%b8%aa%e6%97%b6%e9%97%b4%e6%ae%b5
status: publish
post_type: post

# group by time span  一个时间段

SELECT sum(sizeamount) as counts
    ,[ShopID]
    ,dateadd(hh, - datepart(hour,downloadtime) % 24 ,downloadtime)
    FROM [abc].[dbo].[ShopDownloadAmount]
    group by shopid, dateadd(hh, - datepart(hour,downloadtime) % 24 ,downloadtime)
    order by dateadd(hh, - datepart(hour,downloadtime) % 24 ,downloadtime)
    

  
结果如下  
36730    2    2009-12-15 00:00:00.000  
72342    2    2009-12-16 00:00:00.000  
76858    2    2009-12-17 00:00:00.000  
34094    2    2009-12-18 00:00:00.000  
58178    2    2009-12-19 00:00:00.000