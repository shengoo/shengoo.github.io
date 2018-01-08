title: EntityFramework group by
link: http://www.sheng00.com/938.html
author: admin
description: 
post_id: 938
created: 2013/09/04 00:26:16
created_gmt: 2013/09/03 16:26:16
comment_status: open
post_name: entityframework-group-by
status: private
post_type: post

# EntityFramework group by

[csharp] var query = from p in vavdb.ReportColumnDefinition group p by p.report_id into g select new MyClass { ReportId = g.Key, Count = g.Count(), Names = g.Select(x => x.column_name) }; var sql = query.ToString(); [/csharp]