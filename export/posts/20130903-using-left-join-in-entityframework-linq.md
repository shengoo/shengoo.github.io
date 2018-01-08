title: Using left join in entityframework linq
link: http://www.sheng00.com/934.html
author: admin
description: 
post_id: 934
created: 2013/09/03 15:48:40
created_gmt: 2013/09/03 07:48:40
comment_status: open
post_name: using-left-join-in-entityframework-linq
status: publish
post_type: post

# Using left join in entityframework linq

`from c in table0 join o in table1 on c.sno equals o.sno into ps from o in ps.DefaultIfEmpty() select new { c.name, o.number} `