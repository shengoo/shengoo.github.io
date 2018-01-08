title: .NET中使用nhibernate调用存储过程
link: http://www.sheng00.com/65.html
author: admin
description: 
post_id: 65
created: 1999/11/30 08:00:00
created_gmt: 1999/11/30 00:00:00
comment_status: open
post_name: net%e4%b8%ad%e4%bd%bf%e7%94%a8nhibernate%e8%b0%83%e7%94%a8%e5%ad%98%e5%82%a8%e8%bf%87%e7%a8%8b
status: publish
post_type: post

# .NET中使用nhibernate调用存储过程

映射文件hbm.xml里要  
<sql-query name="Filter_CheckAssignTime">  
<return class="FilterService.Entities.Filter_Course_MediaEntity, FilterService.Entities">  
</return>  
exec Filter_CheckAssignTime  
</sql-query>  
  
dao里调用  
NHibernateSession.GetNamedQuery("Filter_CheckAssignTime").List();