title: NHibernate??????sql°??±?????????á??×??????è??·????à?????????à??
link: http://www.sheng00.com/51.html
author: admin
description: 
post_id: 51
created: 1999/11/30 08:00:00
created_gmt: 1999/11/30 00:00:00
comment_status: open
post_name: nhibernateode%c2%b9oasqle%c2%b1%c2%bca%c2%b6i%c2%bcaeea%c2%bda%c2%b9uxu%c2%bai%c2%b2%c2%a2eeoa%c2%b7%c2%b5%c3%b8aadii%c2%aae%c2%b5iaaadi
status: publish
post_type: post

# NHibernate??????sql°??±?????????á??×??????è??·????à?????????à??

public IList<ShopDownloadAmountEntity> GetDayByShopBetween(int shopID, DateTime startTime, DateTime endTime)  
{  
StringBuilder sb = new StringBuilder();  
sb.Append("SELECT sum(sizeamount) as SizeAmount,[ShopID],");  
  
sb.Append("dateadd(hh, - datepart(hour,downloadtime) % 24 ,downloadtime) as DownloadTime ");  
sb.Append("FROM ShopDownloadAmount ");  
sb.Append("WHERE downloadtime between '" \+ startTime + "' and '" \+ endTime + "'");  
sb.Append(" GROUP BY shopid, dateadd(hh, - datepart(hour,downloadtime) % 24 ,downloadtime) ");  
sb.Append(" order by dateadd(hh, - datepart(hour,downloadtime) % 24 ,downloadtime)");//sql string  
  
ISQLQuery sql = NHibernateSession.CreateSQLQuery(sb.ToString());  
sql.AddScalar("SizeAmount", NHibernateUtil.Int32);//set type of data  
sql.AddScalar("ShopID", NHibernateUtil.Int32);  
sql.AddScalar("DownloadTime", NHibernateUtil.DateTime);  
sql.SetResultTransformer(Transformers.AliasToBean(typeof(ShopDownloadAmountEntity)));//make the result set to entity  
return sql.List<ShopDownloadAmountEntity>();  
}  
ShopDownloadAmountEntity???????à??SizeAmount??ShopID??DownloadTime??setter