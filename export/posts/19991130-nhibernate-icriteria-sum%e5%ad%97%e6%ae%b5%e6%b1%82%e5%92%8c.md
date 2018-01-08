title: Nhibernate ICriteria sum字段求和
link: http://www.sheng00.com/57.html
author: admin
description: 
post_id: 57
created: 1999/11/30 08:00:00
created_gmt: 1999/11/30 00:00:00
comment_status: open
post_name: nhibernate-icriteria-sum%e5%ad%97%e6%ae%b5%e6%b1%82%e5%92%8c
status: publish
post_type: post

# Nhibernate ICriteria sum字段求和

ICriteria criteria = NHibernateSession.CreateCriteria(typeof(DownloadLogEntity));
    criteria.CreateAlias("Enduser", "enduser");
    criteria.Add(Expression.Eq("enduser.EnduserID",enduserID));
    criteria.Add(Expression.Between("DownloadTime", day, day.AddDays(1)));
    criteria.SetProjection(Projections.Sum("FileSize"));
    return (int)criteria.UniqueResult();