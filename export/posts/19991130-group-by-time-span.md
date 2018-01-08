title: group by time span
link: http://www.sheng00.com/54.html
author: admin
description: 
post_id: 54
created: 1999/11/30 08:00:00
created_gmt: 1999/11/30 00:00:00
comment_status: open
post_name: group-by-time-span
status: publish
post_type: post

# group by time span

SELECT count(*), 
    DateAdd(second, -DatePart(second, clientTime) ,  
    DateAdd(ms, -DatePart(ms, clientTime), clientTime))
    FROM dbo.V_COMBINED
    WHERE (sessionId = '122b')
    AND (type = N'sys_goodaction')
    AND (paraName = 'value')
    GROUP BY DateAdd(second, -DatePart(second, clientTime) % 5
    ,DateAdd(ms, -DatePart(ms, clientTime), clientTime))