title: How can I select the first day of a month in SQL?
link: http://www.sheng00.com/997.html
author: admin
description: 
post_id: 997
created: 2013/10/29 17:19:35
created_gmt: 2013/10/29 09:19:35
comment_status: open
post_name: how-can-i-select-the-first-day-of-a-month-in-sql
status: publish
post_type: post

# How can I select the first day of a month in SQL?

SELECT DATEADD(month, DATEDIFF(month, 0, GETDATE()), 0)